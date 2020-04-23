---
layout:     post
title:      opencv-002-色彩空间转换(cvtcolor)与图像保存(imwrite)
subtitle:   学习opencv
date:       2020-04-05
author:     Ancy
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - OpenCV
---

# opencv-002-色彩空间转换(cvtcolor)与图像保存(imwrite)

### 知识点

1. 色彩空间转换函数- cvtColor
   COLOR_BGR2GRAY = 6 彩色到灰度
   COLOR_GRAY2BGR = 8 灰度到彩色
   COLOR_BGR2HSV = 40 BGR到HSV
   COLOR_HSV2BGR = 54 HSV到 BGR
2. 图像保存 - imwrite
   第一个参数是图像保存路径
   第二个参数是图像内存对象

### 代码（c++,python）

```
#include <opencv2/opencv.hpp>
#include <iostream>

using namespace std;
using namespace cv;

int main(){
    Mat src = imread("../images/liuyifei_1.png");

    if (src.empty()){
        cout << "could not load image..." << endl;
        return -1;
    }
    namedWindow("input");
    imshow("input",src);

    Mat dst;
    cvtColor(src,dst,COLOR_BGR2GRAY);
    imwrite("../images/result1.png",dst);
    namedWindow("output gray");
    imshow("output gray",dst);

    waitKey(0);

    return 0;
}
```
```
import cv2 as cv

src = cv.imread("../images/liuyifei_1.png")
cv.namedWindow("input", cv.WINDOW_AUTOSIZE)
cv.imshow("input", src)
gray = cv.cvtColor(src, cv.COLOR_BGR2GRAY)
cv.imshow("gray", gray)
cv.waitKey(0)
cv.destroyAllWindows()
```

### 结果

[![img](http://ww1.sinaimg.cn/large/007cc5tqgy1g19hnk640sj31h00ru7wh.jpg)](http://ww1.sinaimg.cn/large/007cc5tqgy1g19hnk640sj31h00ru7wh.jpg)http://ww1.sinaimg.cn/large/007cc5tqgy1g195s6uz4kj31h70smqlp.jpg)