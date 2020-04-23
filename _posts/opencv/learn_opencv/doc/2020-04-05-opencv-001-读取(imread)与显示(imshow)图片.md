---
layout:     post
title:      opencv-001-读取(imread)与显示(imshow)图像
subtitle:   学习opencv
date:       2020-04-05
author:     Ancy
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - OpenCV
---

## opencv-001-读取(imread)与显示(imshow)图像

### 知识点

- 读取图像 - imread()
- 显示图像 - imshow()

### 代码（c++,python）

```
#include <opencv2/opencv.hpp>
#include <iostream>

using namespace std;
using namespace cv;

int main() {
    // Mat image = imread("../images/liuyifei_1.png");
    // 读取的时候加参数，使读取后为灰度图像
    Mat image = imread("../images/liuyifei_1.png",IMREAD_GRAYSCALE);

    if (image.empty()) {
        cout << "could not load image..." << endl;
        return -1;
    }

    namedWindow("input");
    imshow("input",image);
    waitKey(0);
    return 0;
}
import cv2 as cv

src = cv.imread("../images/liuyifei_1.png")
cv.namedWindow("input", cv.WINDOW_AUTOSIZE)
cv.imshow("input", src)
cv.waitKey(0)
cv.destroyAllWindows()
```

### 结果

[![img](http://ww1.sinaimg.cn/large/007cc5tqgy1g195s6uz4kj31h70smqlp.jpg)](http://ww1.sinaimg.cn/large/007cc5tqgy1g195s6uz4kj31h70smqlp.jpg)