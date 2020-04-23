---
layout:     post   				    # 使用的布局（不需要改）
title:    PYTORCH训练的分割网络模型在OPENCV4.0/C++上部署 				# 标题 
# subtitle:   Hello World, Hello Blog #副标题
date:       2020-03-21 				# 时间
author:    Ancy 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Pytorch
---

## PYTORCH训练的分割网络模型在OPENCV4.0/C++上部署
转载于：http://www.freesion.com/article/8927209235/
        之前把Pytorch训练的分割网络模型用libtorch进行部署折腾了很久，还是很顺利的部署上了，后来换上cuda版本的libtorch速度一下子快多了，比用pytorch做inference要快一些。但是我发布程序的时候不想打包libtorch库（虽然它也很小），于是就尝试仅用OpenCV来部署pytorch模型。

OpenCV4的dnn模块目前支持Caffe，Tensorflow，Onnx，Torch等一些模型的inference。这里的Torch不是Pytorch，而是Pytorch的祖先，基于lua的那个torch，不一样的模型。所以最好是用tensorflow，工业界果然还是TF的天下，话说回来，我还没搞明白TF的pbtxt怎么生成。既然如此，我只能通过模型转换来实现了，转Caffe还是转Onnx呢？我们发现Pytorch天然支持把模型和参数保存成onnx模型。而转Caffe也有第三方开源的程序可以转。我们还是用官方的转onnx吧。

转onnx其实还是很简单的，还得用Python写


```python
import torch
import torch.onnx
from mynet import Mynet
print('Torch Version: ', torch.__version__)
device = torch.device("cuda" if torch.cuda.is_available() else "cpu")
#device = torch.device("cpu")
modeldir = 'D:\\'
modelName = 'weights_99'
modelpath = modelName+'.pth'
onnxmodelname = modelName+'_model_onnx.onnx'
model = Mynet(3, 1).to(device)
checkpoint = torch.load(modeldir + modelpath, map_location=lambda storage, loc: storage.cuda(0))  # 载入weights
model.load_state_dict(checkpoint)  # 用weights初始化网络
example = torch.rand(1, 3, 512, 512).to(device) #输入为512*512的RGB数据
model.eval()
# 转onnx模型
torch.onnx.export(model, example, modeldir + onnxmodelname, verbose=True)
print('Translate end')
```

得到模型和权重文件后，我们就能拿来部署了。我们用QT或者VS2015建一个x64的C++工程，这里为了编码方便，我选了QT吧。

首先在QT的工程文件(.pro)中添加对openCV的包含文件，库文件


```
INCLUDEPATH += \
    D:/OpenCV/opencv410/build/include
debug {
    LIBS += \
        -LD:/OpenCV/opencv410/build/x64/vc15/lib -lopencv_world410d
}
release {
    LIBS += \
        -LD:/OpenCV/opencv410/build/x64/vc15/lib -lopencv_world410
}
```

下面我们看下OpenCV的代码怎么写的，其中大部分从网上抄的



    #include <opencv2/dnn.hpp>
    #include <opencv2/imgproc.hpp>
    #include <opencv2/highgui.hpp>
    using namespace cv;
    using namespace cv::dnn;
    
    #include <fstream>
    #include <iostream>
    #include <cstdlib>
    #include <opencv2/core/ocl.hpp>
    using namespace std;
    
    #include <QDebug>
    
    void test()
    {
    //    cv::dnn::initModule();  //Required if OpenCV is built as static libs
        ocl::setUseOpenCL(false);//关闭OpenCL，就不会出错了
    String modelBin = "D:\\weights_99_model_onnx.onnx";
    String imageFile = "D:\\008.png";
     
    //! [Read and initialize network]
    Net net = dnn::readNetFromONNX(modelBin);
    net.setPreferableBackend(0);	//设置模型的实现方式，分OpenCV和Intel加速
    net.setPreferableTarget(0);	//推断设备选择
     
    //! [Check that network was read successfully]
    if (net.empty())
    {
        std::cerr << "Can't load network by using the following files: " << std::endl;
        std::cerr << "caffemodel: " << modelBin << std::endl;
        std::cerr << "bvlc_googlenet.caffemodel can be downloaded here:" << std::endl;
        std::cerr << "http://dl.caffe.berkeleyvision.org/bvlc_googlenet.caffemodel" << std::endl;
        exit(-1);
    }
     
    //! [Prepare blob]
    Mat img = imread(imageFile);	//加载图片
    if (img.empty())
    {
        std::cerr << "Can't read image from the file: " << imageFile << std::endl;
        exit(-1);
    }
     
    resize(img, img, Size(512, 512));                   //MyNet accepts only 512x512 RGB-images
     
    Mat blob;
    dnn::blobFromImage(img, blob, 1.0, Size(512, 512), Scalar(127,127,127), false, false);	//把图像转成4通道的tensor数据(float)，每个通道的数据都-127
    blob /= 127.0; 	//把数据归一化到(-1,1)
    net.setInput(blob);	//设置输入
     
    clock_t tm =clock();
    Mat output = net.forward();	//进行推断
    tm = clock() - tm;
    qDebug()<<"Cost: "<<tm;
     
    // process output
    std::vector<cv::Mat> ress;
    imagesFromBlob(output, ress); //从Tensor转回ImageMat，这步很重要，要不然不好用cv处理
     
    // show res
    Mat res;
    ress[0] = (ress[0]>0);	//二值化
    ress[0].convertTo(res, CV_8UC1);
     
    //结果以mask的形式与原图合成
    if(res.cols>0)
    {
        res = (res>0);
        cv::Mat res8u;
        res.convertTo(res8u, CV_8UC1);//这步多余的，历史遗留
     
        cv::Mat img = cv::imread(imageFile);
     
        cv::Mat maskImg = cv::Mat::zeros(res8u.rows, res8u.cols, CV_8UC3);
     
        for(int i=0;i<res8u.rows;i++)
        {
            for(int j=0;j<res8u.cols;j++)
            {
                if(res8u.at<uchar>(i,j)>0)
                    maskImg.at<cv::Vec3b>(i, j)=cv::Vec3b(0,0,255);
            }
        }
     
        double alpha = 0.4;
        
        cv::addWeighted(img, 1.0, maskImg, alpha, 0, img);
     
        cv::imshow("a", img);
     
        // imshow之后必须有waitKey函数，否则显示窗内将一闪而过，不会驻留屏幕
        cv::waitKey(0);
     
    }
    return;
    }

qmake & build， 记得把opencv_world410(d).dll拷贝到生成的目录下

![img](http://www.freesion.com/images/89/e3e5dc5ce21dbd61a6b68ecc32b87591.png)


