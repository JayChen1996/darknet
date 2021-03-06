# Yolo-v3 and Yolo-v2 for Windows and Linux
# 在Windows和Linux上训练 YOLOv3 和 YOLOv2
### (neural network for object detection) - Tensor Cores can be used on [Linux](#how-to-compile-on-linux) and [Windows](#how-to-compile-on-windows-using-vcpkg)
### (用于目标检测的神经网络) - Tesor Core可以在 [Linux](#how-to-compile-on-linux)和[Windows](#how-to-compile-on-windows-using-vcpkg)上使用

Contributors: https://github.com/AlexeyAB/darknet/graphs/contributors 
项目贡献者: https://github.com/AlexeyAB/darknet/graphs/contributors 
More details: http://pjreddie.com/darknet/yolo/
更多详情: http://pjreddie.com/darknet/yolo/


[![CircleCI](https://circleci.com/gh/AlexeyAB/darknet.svg?style=svg)](https://circleci.com/gh/AlexeyAB/darknet)
[![TravisCI](https://travis-ci.org/AlexeyAB/darknet.svg?branch=master)](https://travis-ci.org/AlexeyAB/darknet)
[![AppveyorCI](https://ci.appveyor.com/api/projects/status/594bwb5uoc1fxwiu/branch/master?svg=true)](https://ci.appveyor.com/project/AlexeyAB/darknet/branch/master)


* [Requirements (and how to install dependecies)](#requirements)
* [要求 (以及如何安装依赖库)](#requirements_chinese)
* [Pre-trained models](#pre-trained-models)
* [预训练模型](#pre-trained-models_chinese)
* [Explanations in issues](https://github.com/AlexeyAB/darknet/issues?q=is%3Aopen+is%3Aissue+label%3AExplanations)
* [问题解释](https://github.com/AlexeyAB/darknet/issues?q=is%3Aopen+is%3Aissue+label%3AExplanations)

0.  [Improvements in this repository](#improvements-in-this-repository)
0.  [这个repository的改进](#improvements-in-this-repository_chinese)
1.  [How to use](#how-to-use-on-the-command-line)
1.  [如何使用](#how-to-use-on-the-command-line_chinese)
2.  [How to compile on Linux](#how-to-compile-on-linux)
2.  [如何在Linux上编译](#how-to-compile-on-linux_chinese)
3.  How to compile on Windows
3.  如何在Windows上编译
    * [Using vcpkg](#how-to-compile-on-windows-using-vcpkg)
    * [使用vcpkg](#how-to-compile-on-windows-using-vcpkg_chinese)
    * [Legacy way](#how-to-compile-on-windows-legacy-way)
    * [以前版本的编译方法](#how-to-compile-on-windows-legacy-way_chinese)
4.  [How to train (Pascal VOC Data)](#how-to-train-pascal-voc-data)
4.  [如何训练(在Pascal VOC 数据集上)](#how-to-train-pascal-voc-data_chinese)
5.  [How to train with multi-GPU:](#how-to-train-with-multi-gpu)
5.  [如何使用多GPU训练:](#how-to-train-with-multi-gpu_chinese)
6.  [How to train (to detect your custom objects)](#how-to-train-to-detect-your-custom-objects)
6.  [如何训练以检测你自己的目标](#how-to-train-to-detect-your-custom-objects_chinese)
7.  [How to train tiny-yolo (to detect your custom objects)](#how-to-train-tiny-yolo-to-detect-your-custom-objects)
7.  [如何训练tiny-yolo以检测你自己的目标](#how-to-train-tiny-yolo-to-detect-your-custom-objects_chinese)
8.  [When should I stop training](#when-should-i-stop-training)
8.  [什么时候应该停止训练](#when-should-i-stop-training_chinese)
9.  [How to calculate mAP on PascalVOC 2007](#how-to-calculate-map-on-pascalvoc-2007)
9.  [如何在PascalVOC 2007上计算mAP(各类别平均精度的均值,见https://www.zhihu.com/question/53405779)](#how-to-calculate-map-on-pascalvoc-2007)
10.  [How to improve object detection](#how-to-improve-object-detection)
10.  [如何改进目标检测](#how-to-improve-object-detection)
11.  [How to mark bounded boxes of objects and create annotation files](#how-to-mark-bounded-boxes-of-objects-and-create-annotation-files)
11.  [如何标记包选框以及创建相应的标注解释文件(annotation files)](#how-to-mark-bounded-boxes-of-objects-and-create-annotation-files)
12. [How to use Yolo as DLL and SO libraries](#how-to-use-yolo-as-dll-and-so-libraries)
12. [如何将YOLO作为dll或者so这样的动态链接库使用](#how-to-use-yolo-as-dll-and-so-libraries)

(下面是[YOLOv3论文]https://pjreddie.com/media/files/papers/YOLOv3.pdf中的图)

|  ![Darknet Logo](http://pjreddie.com/media/files/darknet-black-small.png) | &nbsp; ![map_time](https://user-images.githubusercontent.com/4096485/52151356-e5d4a380-2683-11e9-9d7d-ac7bc192c477.jpg) mAP@0.5 (AP50) https://pjreddie.com/media/files/papers/YOLOv3.pdf |
|---|---|

* YOLOv3-spp better than YOLOv3 - mAP = 60.6%, FPS = 20: https://pjreddie.com/darknet/yolo/
* YOLOv3-spp版本好于YOLOv3([spp即Spartial Pyramid Pooling](https://medium.com/@arashilen/note-for-yolov3-3e867c0ceca9))--mAP = 60.6%, FPS=20: https://pjreddie.com/darknet/yolo/
* Yolo v3 source chart for the RetinaNet on MS COCO got from Table 1 (e): https://arxiv.org/pdf/1708.02002.pdf
* YOLO v3 论文中的图表(就是上面那个很拉风的图)来源于RetinaNet在MS COCO数据集上的测试论文——Table 1 (e): https://arxiv.org/pdf/1708.02002.pdf
* Yolo v2 on Pascal VOC 2007: https://hsto.org/files/a24/21e/068/a2421e0689fb43f08584de9d44c2215f.jpg
* YOLO v2 在VOC2007上的测试结果(我不是针对各位的那种): https://hsto.org/files/a24/21e/068/a2421e0689fb43f08584de9d44c2215f.jpg
* Yolo v2 on Pascal VOC 2012 (comp4): https://hsto.org/files/3a6/fdf/b53/3a6fdfb533f34cee9b52bdd9bb0b19d9.jpg
* YOLO v2 在Pascal VOC 2012(comp4)上结果(ps.comp4是在其他数据集上训练，comp3是在VOC数据集上训练http://host.robots.ox.ac.uk:8080/leaderboard/main_bootstrap.php): https://hsto.org/files/3a6/fdf/b53/3a6fdfb533f34cee9b52bdd9bb0b19d9.jpg

### Requirements
### 要求

* Windows or Linux
* Windows或者Linux
* **CMake >= 3.8** for modern CUDA support: https://cmake.org/download/
* **Cmake版本>=3.8** 以[支持现有版本的CUDA C++语言](https://devblogs.nvidia.com/building-cuda-applications-cmake/): https://cmake.org/download/
* **CUDA 10.0**: https://developer.nvidia.com/cuda-toolkit-archive (on Linux do [Post-installation Actions](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions))
* **CUDA 10.0**: https://developer.nvidia.com/cuda-toolkit-archive (Linux上必须做一些安装后操作[Post-installation Actions](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions))
* **OpenCV < 4.0**: use your preferred package manager (brew, apt), build from source using [vcpkg](https://github.com/Microsoft/vcpkg) or download from [OpenCV official site](https://opencv.org/releases.html) (on Windows set system variable `OPENCV_DIR` = `C:\opencv\build` - where are the `include` and `x64` folders [image](https://user-images.githubusercontent.com/4096485/53249516-5130f480-36c9-11e9-8238-a6e82e48c6f2.png))
* **OpenCV < 4.0**: 使用你顺手的包管理器(brew, apt), 从源码编译 [vcpkg](https://github.com/Microsoft/vcpkg) or 或者从此处下载 [OpenCV 官网](https://opencv.org/releases.html) (在Windows系统中设置环境变量 `OPENCV_DIR` = `C:\opencv\build` - 为目录 `include` 和 `x64` 所在的地方，如图所示[image](https://user-images.githubusercontent.com/4096485/53249516-5130f480-36c9-11e9-8238-a6e82e48c6f2.png))
* **cuDNN >= 7.0 for CUDA 10.0** https://developer.nvidia.com/rdp/cudnn-archive (on **Linux** copy `cudnn.h`,`libcudnn.so`... as desribed here https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html#installlinux-tar , on **Windows** copy `cudnn.h`,`cudnn64_7.dll`, `cudnn64_7.lib` as desribed here https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html#installwindows )
* **cuDNN >= 7.0 for CUDA 10.0** https://developer.nvidia.com/rdp/cudnn-archive (在 **Linux** 中复制 `cudnn.h`,`libcudnn.so`...到指定位置， 详见 https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html#installlinux-tar , 在 **Windows** 上复制 `cudnn.h`,`cudnn64_7.dll`, `cudnn64_7.lib` 这几个文件到指定位置，详见 https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html#installwindows )
* **GPU with CC >= 3.0**: https://en.wikipedia.org/wiki/CUDA#GPUs_supported
* **GPU with CC >= 3.0**: GPU的算力要大于等于3.0，(CC, Compute Capability)，查看你的CPU的算力:https://en.wikipedia.org/wiki/CUDA#GPUs_supported
* on Linux **GCC or Clang**, on Windows **MSVS 2017 (v15)** https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15#
* Linux上使用 **GCC 或者 Clang**, Windows上则使用 **MSVS 2017 (v15)** https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=15#


#### Pre-trained models
#### 预训练好的模型权重

There are weights-file for different cfg-files (smaller size -> faster speed & lower accuracy:
这些权重文件对应着不同的cfg文件(网络结构配置文件)( 文件越小，速度越快，精确度越低)

* `yolov3-openimages.cfg` (247 MB COCO **Yolo v3**) - requires 4 GB GPU-RAM: https://pjreddie.com/media/files/yolov3-openimages.weights
* `yolov3-openimages.cfg` (247 MB COCO **Yolo v3**) - 需要4GB显卡内存: https://pjreddie.com/media/files/yolov3-openimages.weights
* `yolov3-spp.cfg` (240 MB COCO **Yolo v3**) - requires 4 GB GPU-RAM: https://pjreddie.com/media/files/yolov3-spp.weights
* `yolov3-spp.cfg` (240 MB COCO **Yolo v3**) - 需要4GB显卡内存: https://pjreddie.com/media/files/yolov3-spp.weights
* `yolov3.cfg` (236 MB COCO **Yolo v3**) - requires 4 GB GPU-RAM: https://pjreddie.com/media/files/yolov3.weights
* `yolov3.cfg` (236 MB COCO **Yolo v3**) - 需要4GB显卡内存: https://pjreddie.com/media/files/yolov3.weights
* `yolov3-tiny.cfg` (34 MB COCO **Yolo v3 tiny**) - requires 1 GB GPU-RAM:  https://pjreddie.com/media/files/yolov3-tiny.weights
* `yolov3-tiny.cfg` (34 MB COCO **Yolo v3 tiny**) - 需要1GB显卡内存:  https://pjreddie.com/media/files/yolov3-tiny.weights
* `yolov2.cfg` (194 MB COCO Yolo v2) - requires 4 GB GPU-RAM: https://pjreddie.com/media/files/yolov2.weights
* `yolov2.cfg` (194 MB COCO Yolo v2) - 需要4GB显卡内存: https://pjreddie.com/media/files/yolov2.weights
* `yolo-voc.cfg` (194 MB VOC Yolo v2) - requires 4 GB GPU-RAM: http://pjreddie.com/media/files/yolo-voc.weights
* `yolo-voc.cfg` (194 MB VOC Yolo v2) - 需要4GB显卡内存: http://pjreddie.com/media/files/yolo-voc.weights
* `yolov2-tiny.cfg` (43 MB COCO Yolo v2) - requires 1 GB GPU-RAM: https://pjreddie.com/media/files/yolov2-tiny.weights
* `yolov2-tiny.cfg` (43 MB COCO Yolo v2) - 需要1GB显卡内存: https://pjreddie.com/media/files/yolov2-tiny.weights
* `yolov2-tiny-voc.cfg` (60 MB VOC Yolo v2) - requires 1 GB GPU-RAM: http://pjreddie.com/media/files/yolov2-tiny-voc.weights
* `yolov2-tiny-voc.cfg` (60 MB VOC Yolo v2) - 需要1GB显卡内存: http://pjreddie.com/media/files/yolov2-tiny-voc.weights
* `yolo9000.cfg` (186 MB Yolo9000-model) - requires 4 GB GPU-RAM: http://pjreddie.com/media/files/yolo9000.weights
* `yolo9000.cfg` (186 MB Yolo9000-model) - 需要4GB显卡内存: http://pjreddie.com/media/files/yolo9000.weights

Put it near compiled: darknet.exe
把下载好的权重文件放在darknet.exe同一个目录下(先别去找，你找不到的，darknet.exe是你编译后再生成的)

You can get cfg-files by path: `darknet/cfg/`
你可以通过这个路径: `darknet/cfg/` 来获取.cfg文件(网络结构的配置文件)

##### Examples of results
##### 结果示例

[![Yolo v3](http://img.youtube.com/vi/VOC3huqHrss/0.jpg)](https://www.youtube.com/watch?v=MPU2HistivI "Yolo v3")

Others: https://www.youtube.com/user/pjreddie/videos
其他还有: https://www.youtube.com/user/pjreddie/videos

### Improvements in this repository
### 这个仓库所作的改进

* added support for Windows
* 添加了Windows支持
* improved binary neural network performance **2x-4x times** for Detection on CPU and GPU if you trained your own weights by using this XNOR-net model (bit-1 inference) : https://github.com/AlexeyAB/darknet/blob/master/cfg/yolov3-tiny_xnor.cfg
* 如果你通过使用这个XNOR-net模型(bit-1 inference，这个要看相关文献，我不懂了)https://github.com/AlexeyAB/darknet/blob/master/cfg/yolov3-tiny_xnor.cfg来训练你自己的权重文件，那么改进的二进制神经网络([BNN](https://software.intel.com/en-us/articles/binary-neural-networks))在CPU和GPU上进行的检测任务性能可以提升2到4倍
* improved neural network performance **~7%** by fusing 2 layers into 1: Convolutional + Batch-norm
* 通过融合两层:Convolutional+Batch-norm为一层，提升了神经网络的约7%的性能
* improved neural network performance Detection **3x times**, Training **2 x times** on GPU Volta (Tesla V100, Titan V, ...) using Tensor Cores if `CUDNN_HALF` defined in the `Makefile` or `darknet.sln`
* 如果在`Makefile`或者`darknet.sln`中定义了`CUDNN_HALF`宏，通过使用张量核心(Tensor Cores)可以在Volta架构的GPU上提升网络检测性能**三倍**，训练性能**两倍**
* improved performance **~1.2x** times on FullHD, **~2x** times on 4K, for detection on the video (file/stream) using `darknet detector demo`... 
* 对于视频(文件或流视频)使用`darknet detector demo`检测，在全高清规格上提升了约**1.2倍**性能，4K上提升了**约两倍**性能，
* improved performance **3.5 X times** of data augmentation for training (using OpenCV SSE/AVX functions instead of hand-written functions) - removes bottleneck for training on multi-GPU or GPU Volta
* (使用OpenCV [SSE/AVX](https://zhoujianshi.github.io/articles/2017/%E4%BD%BF%E7%94%A8Intel%20SSE-AVX%E6%8C%87%E4%BB%A4%E9%9B%86%EF%BC%88SIMD%EF%BC%89%E5%8A%A0%E9%80%9F%E5%90%91%E9%87%8F%E5%86%85%E7%A7%AF%E8%AE%A1%E7%AE%97/index.html) 函数而不是手写函数)提升了训练时的数据增强性能**3.5倍** - 打破了在多GPU或者是Volta架构GPU上训练的瓶颈
* improved performance of detection and training on Intel CPU with AVX (Yolo v3 **~85%**, Yolo v2 ~10%)
* 提升了使用了AVX(Advanced Vector Extensions)的英特尔CPU进行检测和训练的性能(Yolo v3 **约85%**, YOLO v2 约10%)
* fixed usage of `[reorg]`-layer
* 修复了`[reorg]`层的用法(具体我还没搞懂，详见https://blog.csdn.net/qq_17550379/article/details/78948839)
* optimized memory allocation during network resizing when `random=1`
* 当`random=1`时在网络resizing(不懂，可能是resize图像吧)期间优化内存分配
* optimized initialization GPU for detection - we use batch=1 initially instead of re-init with batch=1
* 为检测任务优化了GPU初始化 - 我们一开始就使用了batch=1而不是使用batch=1重新初始化
* added correct calculation of **mAP, F1, IoU, Precision-Recall** using command `darknet detector map`...
* 添加了使用**mAP, F1, IoU, Precision-Recall**方式的准确度度量，使用命令 `darknet detector map`可以使用他们
* added drawing of chart of average-Loss and accuracy-mAP (`-map` flag) during training
* 添加了训练期间的average-Loss(平均损失)和准确度度量mAP(`-map` 命令参数可以调用)的图表绘制
* run `./darknet detector demo ... -json_port 8070 -mjpeg_port 8090` as JSON and MJPEG server to get results online over the network by using your soft or Web-browser
* 运行 `./darknet detector demo ... -json_port 8070 -mjpeg_port 8090` 作为JSON和MJPEG服务器以通过你的软件或者浏览器在线获取结果。
* added calculation of anchors for training
* 添加训练时anchors(锚)的计算
* added example of Detection and Tracking objects: https://github.com/AlexeyAB/darknet/blob/master/src/yolo_console_dll.cpp
* 添加了检测和跟踪目标的例子: https://github.com/AlexeyAB/darknet/blob/master/src/yolo_console_dll.cpp
* fixed code for use Web-cam on OpenCV 3.x
* 修复了OpenCV 3.x使用网络摄像头的代码
* run-time tips and warnings if you use incorrect cfg-file or dataset
* 如果你使用了不正确的配置文件或者数据集，可以在运行时给出提示和警告
* many other fixes of code...
* 以及其他很多代码的修正

And added manual - [How to train Yolo v3/v2 (to detect your custom objects)](#how-to-train-to-detect-your-custom-objects)
添加了手册 - [如何训练Yolo v3/v2以检测你自己的目标](#how-to-train-to-detect-your-custom-objects)


Also, you might be interested in using a simplified repository where is implemented INT8-quantization (+30% speedup and -1% mAP reduced): https://github.com/AlexeyAB/yolo2_light
也许，你对通过INT8-quantization技术(30%的速度提升及1%的精度损失)实现的简化版的库更感兴趣: https://github.com/AlexeyAB/yolo2_light

#### How to use on the command line
#### 如何通过命令行使用

On Linux use `./darknet` instead of `darknet.exe`, like this:`./darknet detector test ./cfg/coco.data ./cfg/yolov3.cfg ./yolov3.weights`
在Linux上使用 `./darknet` 而非`darknet.exe`，像这样:`./darknet detector test ./cfg/coco.data ./cfg/yolov3.cfg ./yolov3.weights`

On Linux find executable file `./darknet` in the root directory, while on Windows find it in the directory `\build\darknet\x64` 
在Linux上找到可执行文件 `./darknet` 在**项目的根目录**下，在Windows上你可以在`\build\darknet\x64`这个目录中找到它

**他这里的数据集就是说通过这个数据集训练出来的检测权重和分类，数据集在这个算法产生的结果就在于分类和权重不一样，不同数据集的不同配置文件在coco.data里**
* Yolo v3 COCO - **image**: `darknet.exe detector test cfg/coco.data cfg/yolov3.cfg yolov3.weights -thresh 0.25`
* YOLO v3 COCO数据集 - **图片**: `darknet.exe detector test cfg/coco.data cfg/yolov3.cfg yolov3.weights -thresh 0.25`
* **Output coordinates** of objects: `darknet.exe detector test cfg/coco.data yolov3.cfg yolov3.weights -ext_output dog.jpg`
* **输出检测目标的坐标**: `darknet.exe detector test cfg/coco.data yolov3.cfg yolov3.weights -ext_output dog.jpg`
* Yolo v3 COCO - **video**: `darknet.exe detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights -ext_output test.mp4`
* YOLO v3 COCO数据集 - **视频**: `darknet.exe detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights -ext_output test.mp4`
* Yolo v3 COCO - **WebCam 0**: `darknet.exe detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights -c 0`
* YOLO v3 COCO数据集 - **摄像头**: `darknet.exe detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights -c 0`
* Yolo v3 COCO for **net-videocam** - Smart WebCam: `darknet.exe detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights http://192.168.0.80:8080/video?dummy=param.mjpg`
* YOLO v3 COCO数据集 - **网络视频** - 智能网络摄像头: `darknet.exe detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights http://192.168.0.80:8080/video?dummy=param.mjpg`
* Yolo v3 - **save result videofile res.avi**: `darknet.exe detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test.mp4 -out_filename res.avi`
* Yolo v3 - **保存结果视频文件**: `darknet.exe detector demo cfg/coco.data cfg/yolov3.cfg yolov3.weights test.mp4 -out_filename res.avi`
* Yolo v3 **Tiny** COCO - video: `darknet.exe detector demo cfg/coco.data cfg/yolov3-tiny.cfg yolov3-tiny.weights test.mp4`
* Yolo v3 **Tiny COCO数据集** COCO - 视频检测: `darknet.exe detector demo cfg/coco.data cfg/yolov3-tiny.cfg yolov3-tiny.weights test.mp4`
* **JSON and MJPEG server** that allows multiple connections from your soft or Web-browser `ip-address:8070` and 8090: `./darknet detector demo ./cfg/coco.data ./cfg/yolov3.cfg ./yolov3.weights test50.mp4 -json_port 8070 -mjpeg_port 8090 -ext_output`
* 这里的JSON和MJPEG服务器还没有搞懂
* Yolo v3 Tiny **on GPU #1**: `darknet.exe detector demo cfg/coco.data cfg/yolov3-tiny.cfg yolov3-tiny.weights -i 1 test.mp4`
* YOLOv3的tiny版本 **在GPU #1上**: `darknet.exe detector demo cfg/coco.data cfg/yolov3-tiny.cfg yolov3-tiny.weights -i 1 test.mp4`
* Alternative method Yolo v3 COCO - image: `darknet.exe detect cfg/yolov3.cfg yolov3.weights -i 0 -thresh 0.25`

* Train on **Amazon EC2**, to see mAP & Loss-chart using URL like: `http://ec2-35-160-228-91.us-west-2.compute.amazonaws.com:8090` in the Chrome/Firefox: 
    `./darknet detector train cfg/coco.data yolov3.cfg darknet53.conv.74 -dont_show -mjpeg_port 8090 -map`
* 186 MB Yolo9000 - image: `darknet.exe detector test cfg/combine9k.data yolo9000.cfg yolo9000.weights`
* Remeber to put data/9k.tree and data/coco9k.map under the same folder of your app if you use the cpp api to build an app
* To process a list of images `data/train.txt` and save results of detection to `result.txt` use:                             
    `darknet.exe detector test cfg/coco.data yolov3.cfg yolov3.weights -dont_show -ext_output < data/train.txt > result.txt`
* Pseudo-lableing - to process a list of images `data/new_train.txt` and save results of detection in Yolo training format for each image as label `<image_name>.txt` (in this way you can increase the amount of training data) use:
    `darknet.exe detector test cfg/coco.data yolov3.cfg yolov3.weights -thresh 0.25 -dont_show -save_labels < data/new_train.txt`
* To calculate anchors: `darknet.exe detector calc_anchors data/obj.data -num_of_clusters 9 -width 416 -height 416`
* To check accuracy mAP@IoU=50: `darknet.exe detector map data/obj.data yolo-obj.cfg backup\yolo-obj_7000.weights`
* To check accuracy mAP@IoU=75: `darknet.exe detector map data/obj.data yolo-obj.cfg backup\yolo-obj_7000.weights -iou_thresh 0.75`

##### For using network video-camera mjpeg-stream with any Android smartphone

1. Download for Android phone mjpeg-stream soft: IP Webcam / Smart WebCam

    * Smart WebCam - preferably: https://play.google.com/store/apps/details?id=com.acontech.android.SmartWebCam2
    * IP Webcam: https://play.google.com/store/apps/details?id=com.pas.webcam

2. Connect your Android phone to computer by WiFi (through a WiFi-router) or USB
3. Start Smart WebCam on your phone
4. Replace the address below, on shown in the phone application (Smart WebCam) and launch:

* Yolo v3 COCO-model: `darknet.exe detector demo data/coco.data yolov3.cfg yolov3.weights http://192.168.0.80:8080/video?dummy=param.mjpg -i 0`

### How to compile on Linux
### 如何在Linux上编译

Just do `make` in the darknet directory.
在darknet目录下运行make命令就可以了
Before make, you can set such options in the `Makefile`: [link](https://github.com/AlexeyAB/darknet/blob/9c1b9a2cf6363546c152251be578a21f3c3caec6/Makefile#L1)
在make之前，你可以在`Makefile`中设置选项:[link](https://github.com/AlexeyAB/darknet/blob/9c1b9a2cf6363546c152251be578a21f3c3caec6/Makefile#L1)
* `GPU=1` to build with CUDA to accelerate by using GPU (CUDA should be in `/usr/local/cuda`)
* `GPU=1`表示同CUDA一起构建使用GPU加速(CUDA应该在`/usr/local/cuda`目录中)
* `CUDNN=1` to build with cuDNN v5-v7 to accelerate training by using GPU (cuDNN should be in `/usr/local/cudnn`)
* `CUDNN=1`表示同cuDNN v5-v7一起构建使用GPU加速
* `CUDNN_HALF=1` to build for Tensor Cores (on Titan V / Tesla V100 / DGX-2 and later) speedup Detection 3x, Training 2x
* `CUDNN_HALF=1`可以使用TensorCores(在Titan V/Tesla V100/DGX-2或更新的显卡上)加速，提升检测速度3倍，训练速度2倍
* `OPENCV=1` to build with OpenCV 3.x/2.4.x - allows to detect on video files and video streams from network cameras or web-cams
* `OPENCV=1`表示可以同OpenCV3.x/2.4.x一起构建，允许检测网络摄像头的视频文件和视频流
* `DEBUG=1` to bould debug version of Yolo
* `DEBUG=1`构建YOLO的debug版本
* `OPENMP=1` to build with OpenMP support to accelerate Yolo by using multi-core CPU
* `OPENMP=1`提供OpenMP支持用以使用多CPU加速
* `LIBSO=1` to build a library `darknet.so` and binary runable file `uselib` that uses this library. Or you can try to run so `LD_LIBRARY_PATH=./:$LD_LIBRARY_PATH ./uselib test.mp4` How to use this SO-library from your own code - you can look at C++ example: https://github.com/AlexeyAB/darknet/blob/master/src/yolo_console_dll.cpp
* `LIBSO=1`构建库`darknet.so`和二进制可运行文件`uselib`来使用该库，或者你可以试一试运行so`LD_LIBRARY_PATH=./:$LD_LIBRARY_PATH ./uselib test.mp4`,怎样在你自己的代码中使用这个动态链接库，可以查看C++例子https://github.com/AlexeyAB/darknet/blob/master/src/yolo_console_dll.cpp
    or use in such a way: `LD_LIBRARY_PATH=./:$LD_LIBRARY_PATH ./uselib data/coco.names cfg/yolov3.cfg yolov3.weights test.mp4`
    或者这样使用`LD_LIBRARY_PATH=./:$LD_LIBRARY_PATH ./uselib data/coco.names cfg/yolov3.cfg yolov3.weights test.mp4`
To run Darknet on Linux use examples from this article, just use `./darknet` instead of `darknet.exe`, i.e. use this command: `./darknet detector test ./cfg/coco.data ./cfg/yolov3.cfg ./yolov3.weights`
在Linux上运行Darknet，可以使用本文中的示例，仅需将`darknet.exe`换成`./darknet`，如:`./darknet detector test ./cfg/coco.data ./cfg/yolov3.cfg ./yolov3.weights`
### How to compile on Windows (using `vcpkg`)
### Windows上如何进行编译(使用 `vcpkg`)

1. Install or update Visual Studio to at least version 2017, making sure to have it fully patched (run again the installer if not sure to automatically update to latest version). If you need to install from scratch, download VS from here: [Visual Studio 2017 Community](http://visualstudio.com)
1. 安装或升级Visual Studio到至少VS2017，确保安装了所有的补丁(如果不确认是否升级到最新版本，重新运行一次安装程序)，如果你需要从头安装(install from scratch)，下载VS[Visual Studio 2017 Community](http://visualstudio.com)

2. Install CUDA and cuDNN
2. 安装CUDA和cuDNN

3. Install `git` and `cmake`. Make sure they are on the Path at least for the current account
3. 安装 `git` 和 `cmake`。确保其在环境变量Path中

4. Install [vcpkg](https://github.com/Microsoft/vcpkg) and try to install a test library to make sure everything is working, for example `vcpkg install opengl`
4. 安装 [vcpkg](https://github.com/Microsoft/vcpkg) 并且试着安装一个测试库以确保工作正常，例如`vcpkg install opengl`

5. Define an environment variables, `VCPKG_ROOT`, pointing to the install path of `vcpkg`
5. 定义一个环境变量，`VCPKG_ROOT`, pointing to the install path of `vcpkg`

6. Define another environment variable, with name `VCPKG_DEFAULT_TRIPLET` and value `x64-windows`
6. 再定义一个环境变量，变量名`VCPKG_DEFAULT_TRIPLET`和值`x64-windows`

7. Open a Powershell (as a standard user) and type (the last command requires a confirmation and is used to clean up unnecessary files)
7. 打开powershell，输入如下内容

```PowerShell
PS \>                  cd $env:VCPKG_ROOT
PS Code\vcpkg>         .\vcpkg install pthreads opencv #replace with opencv[cuda] in case you want to use cuda-accelerated openCV
```

8. [necessary only with CUDA] Customize the `build.ps1` script enabling the appropriate `my_cuda_compute_model` line. If not manually defined, CMake toolchain will automatically use the very low 3.0 CUDA compute model
8. [只有CUDA有必要]修改`build.ps1`脚本以适用自己的电脑，将合适的`my_cuda_compute_model`行解除注释，如果没有手动定义，CMake工具将自动使用非常低的3.0版本的CUDA计算模型

9.  Build with the Powershell script `build.ps1`. If you want to use Visual Studio, you will find a custom solution created for you by CMake after the build containing all the appropriate config flags for your system.
9. 用Powershell脚本`build.ps1`进行构建，如果你想要使用Visual Studio，在构建之后，你将会发现一个由CMake创建的包含所有合适于你系统配置的客制的解决方案


### How to compile on Windows (legacy way)
### 如何在Windows上编译(以前的方法)

1. If you have **MSVS 2015, CUDA 10.0, cuDNN 7.4 and OpenCV 3.x** (with paths: `C:\opencv_3.0\opencv\build\include` & `C:\opencv_3.0\opencv\build\x64\vc14\lib`), then start MSVS, open `build\darknet\darknet.sln`, set **x64** and **Release** https://hsto.org/webt/uh/fk/-e/uhfk-eb0q-hwd9hsxhrikbokd6u.jpeg and do the: Build -> Build darknet. Also add Windows system variable `CUDNN` with path to CUDNN: https://user-images.githubusercontent.com/4096485/53249764-019ef880-36ca-11e9-8ffe-d9cf47e7e462.jpg **NOTE:** If installing OpenCV, use OpenCV 3.4.0 or earlier. This is a bug in OpenCV 3.4.1 in the C API (see [#500](https://github.com/AlexeyAB/darknet/issues/500)).
1. 如果你已经安装了**MSVS 2015, CUDA 10.0, cuDNN 7.4 and OpenCV 3.x**（路径:`C:\opencv_3.0\opencv\build\include` & `C:\opencv_3.0\opencv\build\x64\vc14\lib`）,启动MSVS，打开`build\darknet\darknet.sln`，设置**x64** 和 **Release**https://hsto.org/webt/uh/fk/-e/uhfk-eb0q-hwd9hsxhrikbokd6u.jpeg ，接着：Build -> Build darknet。并且在Windows系统上添加了系统变量`CUDNN` 且有合适的路径: https://user-images.githubusercontent.com/4096485/53249764-019ef880-36ca-11e9-8ffe-d9cf47e7e462.jpg  **注意:** 如果安装OpenCV, 使用 OpenCV 3.4.0 或者更早的版本. OpenCV3.4.1在C API上存在一个bug (详见 [#500](https://github.com/AlexeyAB/darknet/issues/500)).

    1.1. Find files `opencv_world320.dll` and `opencv_ffmpeg320_64.dll` (or `opencv_world340.dll` and `opencv_ffmpeg340_64.dll`) in `C:\opencv_3.0\opencv\build\x64\vc14\bin` and put it near with `darknet.exe`
    1.1. 找到文件 `opencv_world320.dll` 和 `opencv_ffmpeg320_64.dll` (或者 `opencv_world340.dll` 和 `opencv_ffmpeg340_64.dll`) 在目录 `C:\opencv_3.0\opencv\build\x64\vc14\bin`中 并且将其拷贝到 `darknet.exe` 同级目录下
    
    1.2 Check that there are `bin` and `include` folders in the `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0` if aren't, then copy them to this folder from the path where is CUDA installed
    1.2 检查`C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0`中是否有 `bin` and `include` 目录，如果没有，从CUDA的安装路径中拷贝过去
    
    1.3. To install CUDNN (speedup neural network), do the following:
    1.3. 要安装CUDNN(用于加速神经网络)，按如下操作
      
    * download and install **cuDNN v7.4.1 for CUDA 10.0**: https://developer.nvidia.com/rdp/cudnn-archive
    * 下载并安装 **cuDNN v7.4.1 for CUDA 10.0**: https://developer.nvidia.com/rdp/cudnn-archive
      
    * add Windows system variable `CUDNN` with path to CUDNN: https://user-images.githubusercontent.com/4096485/53249764-019ef880-36ca-11e9-8ffe-d9cf47e7e462.jpg
    * 添加Windows系统变量 `CUDNN`， 值为CUDNN的路径： https://user-images.githubusercontent.com/4096485/53249764-019ef880-36ca-11e9-8ffe-d9cf47e7e462.jpg
    
    * copy file `cudnn64_7.dll` to the folder `\build\darknet\x64` near with `darknet.exe`
    * 拷贝文件 `cudnn64_7.dll` 到目录 `\build\darknet\x64`在`darknet.exe`旁边
    
    1.4. If you want to build **without CUDNN** then: open `\darknet.sln` -> (right click on project) -> properties  -> C/C++ -> Preprocessor -> Preprocessor Definitions, and remove this: `CUDNN;`
    1.4. 如果你要构建项目且 **不使用CUDNN库**， 那么: 打开 `\darknet.sln` -> (右键单击项目) -> 属性 -> C/C++ -> 预处理器 -> 预处理器定义, 并移除： `CUDNN;`

2. If you have other version of **CUDA (not 10.0)** then open `build\darknet\darknet.vcxproj` by using Notepad, find 2 places with "CUDA 10.0" and change it to your CUDA-version. Then open `\darknet.sln` -> (right click on project) -> properties  -> CUDA C/C++ -> Device and remove there `;compute_75,sm_75`. Then do step 1
2. 如果你使用其他版本的 **CUDA (非 10.0)** 那么使用记事本或其他文本编辑工具打开 `build\darknet\darknet.vcxproj` , 找到 "CUDA 10.0"出现 的两个地方并将其变成你自己的CUDA版本. 然后打开 `\darknet.sln` -> (右键单击项目) -> 属性 -> CUDA C/C++ -> Device 移除 `;compute_75,sm_75`. 然后重复第一步

3. 如果你**没有GPU**,但是有 **MSVS 2015 和 OpenCV 3.0** (安装于路径: `C:\opencv_3.0\opencv\build\include` & `C:\opencv_3.0\opencv\build\x64\vc14\lib`), 那么启动MSVS, 打开 `build\darknet\darknet_no_gpu.sln`, 设置 **x64** 和 **Release**, 然后进行构建: Build -> Build darknet_no_gpu

4. 如果你有 **OpenCV 2.4.13** 而非3.0 ，那么你应该修改库的路径，打开 `\darknet.sln` 后，进行如下两步操作

    4.1 (right click on project) -> properties  -> C/C++ -> General -> Additional Include Directories:  `C:\opencv_2.4.13\opencv\build\include`
  
    4.2 (right click on project) -> properties  -> Linker -> General -> Additional Library Directories: `C:\opencv_2.4.13\opencv\build\x64\vc14\lib`
    
5. If you have GPU with Tensor Cores (nVidia Titan V / Tesla V100 / DGX-2 and later) speedup Detection 3x, Training 2x:
    `\darknet.sln` -> (right click on project) -> properties -> C/C++ -> Preprocessor -> Preprocessor Definitions, and add here: `CUDNN_HALF;`
5. 如果你拥有带Tensor核心的GPU (nVidia Titan V / Tesla V100 / DGX-2 and later) 检测速度会提升三倍，训练提升两倍:
    `\darknet.sln` -> (right click on project) -> properties -> C/C++ -> Preprocessor -> Preprocessor Definitions, 并添加: `CUDNN_HALF;`
    
    **Note:** CUDA must be installed only after that MSVS2015 had been installed.
    **注意：** CUDA必须在安装MSVS2015后安装

### How to compile (custom):
### 如何编译(自定义):

Also, you can to create your own `darknet.sln` & `darknet.vcxproj`, this example for CUDA 9.1 and OpenCV 3.0
当然，你也可以创建你自己的`darknet.sln`和`darknet.vcxproj`,以CUDA9.1和OpenCV3.0为例

Then add to your created project:
加入你自己创建的工程中
- (right click on project) -> properties  -> C/C++ -> General -> Additional Include Directories, put here: 

`C:\opencv_3.0\opencv\build\include;..\..\3rdparty\include;%(AdditionalIncludeDirectories);$(CudaToolkitIncludeDir);$(CUDNN)\include`
- (右键单击项目)->属性-> C/C++ -> 常规 -> 附加包含目录,加入如下的内容
`C:\opencv_3.0\opencv\build\include;..\..\3rdparty\include;%(AdditionalIncludeDirectories);$(CudaToolkitIncludeDir);$(CUDNN)\include`
- (right click on project) -> Build dependecies -> Build Customizations -> set check on CUDA 9.1 or what version you have - for example as here: http://devblogs.nvidia.com/parallelforall/wp-content/uploads/2015/01/VS2013-R-5.jpg
- (右键单击项目)->
- add to project:
    * all `.c` files
    * all `.cu` files 
    * file `http_stream.cpp` from `\src` directory
    * file `darknet.h` from `\include` directory
- (right click on project) -> properties  -> Linker -> General -> Additional Library Directories, put here: 

`C:\opencv_3.0\opencv\build\x64\vc14\lib;$(CUDA_PATH)\lib\$(PlatformName);$(CUDNN)\lib\x64;%(AdditionalLibraryDirectories)`

-  (right click on project) -> properties  -> Linker -> Input -> Additional dependecies, put here: 

`..\..\3rdparty\lib\x64\pthreadVC2.lib;cublas.lib;curand.lib;cudart.lib;cudnn.lib;%(AdditionalDependencies)`
- (right click on project) -> properties -> C/C++ -> Preprocessor -> Preprocessor Definitions

`OPENCV;_TIMESPEC_DEFINED;_CRT_SECURE_NO_WARNINGS;_CRT_RAND_S;WIN32;NDEBUG;_CONSOLE;_LIB;%(PreprocessorDefinitions)`

- compile to .exe (X64 & Release) and put .dll-s near with .exe: https://hsto.org/webt/uh/fk/-e/uhfk-eb0q-hwd9hsxhrikbokd6u.jpeg

    * `pthreadVC2.dll, pthreadGC2.dll` from \3rdparty\dll\x64

    * `cusolver64_91.dll, curand64_91.dll, cudart64_91.dll, cublas64_91.dll` - 91 for CUDA 9.1 or your version, from C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.1\bin

    * For OpenCV 3.2: `opencv_world320.dll` and `opencv_ffmpeg320_64.dll` from `C:\opencv_3.0\opencv\build\x64\vc14\bin` 
    * For OpenCV 2.4.13: `opencv_core2413.dll`, `opencv_highgui2413.dll` and `opencv_ffmpeg2413_64.dll` from  `C:\opencv_2.4.13\opencv\build\x64\vc14\bin`

## How to train (Pascal VOC Data):
## 如何进行训练（Pascal VOC 数据集):

1. Download pre-trained weights for the convolutional layers (154 MB): http://pjreddie.com/media/files/darknet53.conv.74 and put to the directory `build\darknet\x64`
1. 下载卷积层的预训练权重 (154 MB): http://pjreddie.com/media/files/darknet53.conv.74 放到目录`build\darknet\x64`下

2. Download The Pascal VOC Data and unpack it to directory `build\darknet\x64\data\voc` will be created dir `build\darknet\x64\data\voc\VOCdevkit\`:
2. 下载Pascal VOC数据集并解压到目录 `build\darknet\x64\data\voc` 将被创建目录 `build\darknet\x64\data\voc\VOCdevkit\`:
    * http://pjreddie.com/media/files/VOCtrainval_11-May-2012.tar
    * http://pjreddie.com/media/files/VOCtrainval_06-Nov-2007.tar
    * http://pjreddie.com/media/files/VOCtest_06-Nov-2007.tar
    
    2.1 Download file `voc_label.py` to dir `build\darknet\x64\data\voc`: http://pjreddie.com/media/files/voc_label.py
    2.1 下载文件`voc_label.py`到目录 `build\darknet\x64\data\voc`: http://pjreddie.com/media/files/voc_label.py

3. Download and install Python for Windows: https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe
3. 下载并安装Windows下的python: https://www.python.org/ftp/python/3.5.2/python-3.5.2-amd64.exe

4. Run command: `python build\darknet\x64\data\voc\voc_label.py` (to generate files: 2007_test.txt, 2007_train.txt, 2007_val.txt, 2012_train.txt, 2012_val.txt)
4. 运行命令: `python build\darknet\x64\data\voc\voc_label.py` (产生文件: 2007_test.txt, 2007_train.txt, 2007_val.txt, 2012_train.txt, 2012_val.txt)

5. Run command: `type 2007_train.txt 2007_val.txt 2012_*.txt > train.txt`
5. 运行命令: `type 2007_train.txt 2007_val.txt 2012_*.txt > train.txt`

6. Set `batch=64` and `subdivisions=8` in the file `yolov3-voc.cfg`: [link](https://github.com/AlexeyAB/darknet/blob/ee38c6e1513fb089b35be4ffa692afd9b3f65747/cfg/yolov3-voc.cfg#L3-L4)
6. 设置 `batch=64` 和 `subdivisions=8` 在配置文件 `yolov3-voc.cfg` 中: [link](https://github.com/AlexeyAB/darknet/blob/ee38c6e1513fb089b35be4ffa692afd9b3f65747/cfg/yolov3-voc.cfg#L3-L4)

7. Start training by using `train_voc.cmd` or by using the command line: 
7. 使用`train_voc.cmd`或者使用如下命令行开始训练: 

    `darknet.exe detector train cfg/voc.data cfg/yolov3-voc.cfg darknet53.conv.74` 

(**Note:** To disable Loss-Window use flag `-dont_show`. If you are using CPU, try `darknet_no_gpu.exe` instead of `darknet.exe`.)
(**注意:** 关闭损失显示窗口使用参数 `-dont_show`. 如果你使用CPU，那么使用 `darknet_no_gpu.exe` 而非 `darknet.exe`.)

If required change pathes in the file `build\darknet\cfg\voc.data`

More information about training by the link: http://pjreddie.com/darknet/yolo/#train-voc

 **Note:** If during training you see `nan` values for `avg` (loss) field - then training goes wrong, but if `nan` is in some other lines - then training goes well.

## How to train with multi-GPU:

1. Train it first on 1 GPU for like 1000 iterations: `darknet.exe detector train cfg/voc.data cfg/yolov3-voc.cfg darknet53.conv.74`

2. Then stop and by using partially-trained model `/backup/yolov3-voc_1000.weights` run training with multigpu (up to 4 GPUs): `darknet.exe detector train cfg/voc.data cfg/yolov3-voc.cfg /backup/yolov3-voc_1000.weights -gpus 0,1,2,3`

Only for small datasets sometimes better to decrease learning rate, for 4 GPUs set `learning_rate = 0.00025` (i.e. learning_rate = 0.001 / GPUs). In this case also increase 4x times `burn_in =` and `max_batches =` in your cfg-file. I.e. use `burn_in = 4000` instead of `1000`. Same goes for `steps=` if `policy=steps` is set.

https://groups.google.com/d/msg/darknet/NbJqonJBTSY/Te5PfIpuCAAJ

## How to train (to detect your custom objects):
## 如何训练(以检测你自己的物体)
(训练旧的 Yolo v2 `yolov2-voc.cfg`, `yolov2-tiny-voc.cfg`, `yolo-voc.cfg`, `yolo-voc.2.0.cfg`, ... [点击这个链接](https://github.com/AlexeyAB/darknet/tree/47c7af1cea5bbdedf1184963355e6418cb8b1b4f#how-to-train-pascal-voc-data))

Training Yolo v3:
训练YOLOv3：

1. Create file `yolo-obj.cfg` with the same content as in `yolov3.cfg` (or copy `yolov3.cfg` to `yolo-obj.cfg)` and:
1. 直接拷贝文件 `yolov3.cfg` 然后改名为yolo-obj.cfg，然后：

  * 修改batch那一行为 [`batch=64`](https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L3)
  * 修改subdivision那一行为[`subdivisions=8`](https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L4)
  * 修改classes那一行 `classes=80` 为你自己检测的目标种类数目在每个`[yolo]`层中(一共三个yolo层)::
      * https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L610
      * https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L696
      * https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L783
  * 修改 [`filters=255`] 为 filters=(classes + 5)x3 [yolo]层之前的在3个 `[convolutional]`中
      * https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L603
      * https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L689
      * https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L776

  所以如果 `classes=1`那么`filters=18`.如果`classes=2` 那么`filters=21`.
  
  **(Do not write in the cfg-file: filters=(classes + 5)x3)**
  
  (Generally `filters` depends on the `classes`, `coords` and number of `mask`s, i.e. filters=`(classes + coords + 1)*<number of mask>`, where `mask` is indices of anchors. If `mask` is absence, then filters=`(classes + coords + 1)*num`)

  So for example, for 2 objects, your file `yolo-obj.cfg` should differ from `yolov3.cfg` in such lines in each of **3** [yolo]-layers:

  ```
  [convolutional]
  filters=21

  [region]
  classes=2
  ```

2. Create file `obj.names` in the directory `build\darknet\x64\data\`, with objects names - each in new line
2. 创建文件`obj.names`在目录`build\darknet\x64\data\`中，每行一个目标种类名

3. Create file `obj.data` in the directory `build\darknet\x64\data\`, containing (where **classes = number of objects**):
3. 创建文件`obj.data` 在目录 `build\darknet\x64\data\`中，包含如下内容

  ```
  classes= 2
  train  = data/train.txt
  valid  = data/test.txt
  names = data/obj.names
  backup = backup/
  ```

4. Put image-files (.jpg) of your objects in the directory `build\darknet\x64\data\obj\`
4. 将你的检测目标的图片文件(.jpg)放到目录`build\darknet\x64\data\obj\`

5. You should label each object on images from your dataset. Use this visual GUI-software for marking bounded boxes of objects and generating annotation files for Yolo v2 & v3: https://github.com/AlexeyAB/Yolo_mark
5. 你应该标注你数据集的图片中的每个目标. 使用这个可视化的图形界面软件来标注图片中的每个目标并且产生用于yolo v2和v3的解释文件: https://github.com/AlexeyAB/Yolo_mark

It will create `.txt`-file for each `.jpg`-image-file - in the same directory and with the same name, but with `.txt`-extension, and put to file: object number and object coordinates on this image, for each object in new line: 
它会为每个`.jpg`图片文件创建一个 `.txt`文件 - 在相同目录且名字相同仅后缀名不同, 且在相应`.txt` 写入目标数量和在图片中的坐标，一个目标一行: 

`<object-class> <x_center> <y_center> <width> <height>`

  Where: 
  * `<object-class>` - 整型目标类别编号 `0` 到 `(classes-1)`
  * `<x_center> <y_center> <width> <height>` - 浮点型 **相对** 于图片的宽和高, 取值从 `(0.0 到 1.0]`
  * for example: `<x> = <absolute_x> / <image_width>` or `<height> = <absolute_height> / <image_height>`
  * atention: `<x_center> <y_center>` - are center of rectangle (are not top-left corner)
  * 注意: `<x_center> <y_center>` 是矩框的中心，而不是左上角

  For example for `img1.jpg` you will be created `img1.txt` containing:

  ```
  1 0.716797 0.395833 0.216406 0.147222
  0 0.687109 0.379167 0.255469 0.158333
  1 0.420312 0.395833 0.140625 0.166667
  ```

6. Create file `train.txt` in directory `build\darknet\x64\data\`, with filenames of your images, each filename in new line, with path relative to `darknet.exe`, for example containing:
6. 创建文件`train.txt` 在目录`build\darknet\x64\data\`中，内容是你的图片的文件名，一行一个文件名，相对于darknet.txt

  ```
  data/obj/img1.jpg
  data/obj/img2.jpg
  data/obj/img3.jpg
  ```

7. Download pre-trained weights for the convolutional layers (154 MB): https://pjreddie.com/media/files/darknet53.conv.74 and put to the directory `build\darknet\x64`
7. 下载卷积层的预训练权重(154MB):https://pjreddie.com/media/files/darknet53.conv.74 ，并且放到目录`build\darknet\x64`之中

8. Start training by using the command line: `darknet.exe detector train data/obj.data yolo-obj.cfg darknet53.conv.74`
8. 使用命令行: `darknet.exe detector train data/obj.data yolo-obj.cfg darknet53.conv.74`开始进行训练
     
   To train on Linux use command: `./darknet detector train data/obj.data yolo-obj.cfg darknet53.conv.74` (just use `./darknet` instead of `darknet.exe`)
   在Linux上训练使用命令： `./darknet detector train data/obj.data yolo-obj.cfg darknet53.conv.74` (just use `./darknet` instead of `darknet.exe`)
     
   * (file `yolo-obj_last.weights` will be saved to the `build\darknet\x64\backup\` for each 100 iterations)
   * (文件 `yolo-obj_last.weights`每经过100次迭代会被保存到`build\darknet\x64\backup\`）
   * (file `yolo-obj_xxxx.weights` will be saved to the `build\darknet\x64\backup\` for each 1000 iterations)
   * (文件 `yolo-obj_xxxx.weights` 会被保存到 `build\darknet\x64\backup\` 每经过1000次迭代)
   * (to disable Loss-Window use `darknet.exe detector train data/obj.data yolo-obj.cfg darknet53.conv.74 -dont_show`, if you train on computer without monitor like a cloud Amazon EC2)
   * (关闭Loss-Window 使用`darknet.exe detector train data/obj.data yolo-obj.cfg darknet53.conv.74 -dont_show`, 如果你在没有显示器的主机如亚马逊云EC2上训练时)
   * (to see the mAP & Loss-chart during training on remote server without GUI, use command `darknet.exe detector train data/obj.data yolo-obj.cfg darknet53.conv.74 -dont_show -mjpeg_port 8090 -map` then open URL `http://ip-address:8090` in Chrome/Firefox browser)
   * (为了在没有GUI界面的远端服务器上查看训练时的mAP 及 Loss-chart , 使用命令`darknet.exe detector train data/obj.data yolo-obj.cfg darknet53.conv.74 -dont_show -mjpeg_port 8090 -map` 然后打开路径 `http://ip-address:8090` 用谷歌或者火狐浏览器)

8.1. For training with mAP (mean average precisions) calculation for each 4 Epochs (set `valid=valid.txt` or `train.txt` in `obj.data` file) and run: `darknet.exe detector train data/obj.data yolo-obj.cfg darknet53.conv.74 -map`
8.1. 为了训练时每4个Epoch计算一次mAP (设置 `valid=valid.txt` or `train.txt` in `obj.data` file) and 运行: `darknet.exe detector train data/obj.data yolo-obj.cfg darknet53.conv.74 -map`

9. After training is complete - get result `yolo-obj_final.weights` from path `build\darknet\x64\backup\`
9. 训练完成后，从路径 `build\darknet\x64\backup\` 得到结果 `yolo-obj_final.weights`

 * After each 100 iterations you can stop and later start training from this point. For example, after 2000 iterations you can stop training, and later just copy `yolo-obj_2000.weights` from `build\darknet\x64\backup\` to `build\darknet\x64\` and start training using: `darknet.exe detector train data/obj.data yolo-obj.cfg yolo-obj_2000.weights`
 * 每100次迭代后你可以停止并且下次从这里开始训练，2000次迭代后你可以停止训练然后从`build\darknet\x64\backup\` 拷贝 `yolo-obj_2000.weights` 到 `build\darknet\x64\` 然后开始训练: `darknet.exe detector train data/obj.data yolo-obj.cfg yolo-obj_2000.weights`
 

    (in the original repository https://github.com/pjreddie/darknet the weights-file is saved only once every 10 000 iterations `if(iterations > 1000)`)

 * Also you can get result earlier than all 45000 iterations.
 
 **Note:** If during training you see `nan` values for `avg` (loss) field - then training goes wrong, but if `nan` is in some other lines - then training goes well.
 **注意** 如果训练中你看到 `avg` 为 `nan`, 那么训练出现了错误，但如果 `nan` 是在其他行，那么训练未出错。
 
 **Note:** If you changed width= or height= in your cfg-file, then new width and height must be divisible by 32.
 **注意：** 如果你在cfg文件中修改了width= 或者 height= ，那么新的width和height值必须能够被32整除
 
 **Note:** After training use such command for detection: `darknet.exe detector test data/obj.data yolo-obj.cfg yolo-obj_8000.weights`
 **注意** 在训练之后，使用如下命令进行检测： `darknet.exe detector test data/obj.data yolo-obj.cfg yolo-obj_8000.weights`
 
  **Note:** if error `Out of memory` occurs then in `.cfg`-file you should increase `subdivisions=16`, 32 or 64: [link](https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L4)
  **注意：** 如果出现 `Out of memory` 的错误， 在 `.cfg`文件中你应该增加 `subdivisions=16`, 32 or 64: [link](https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L4)
 
### How to train tiny-yolo (to detect your custom objects):
### 如何训练tiny-yolo(检测自定义的目标)

Do all the same steps as for the full yolo model as described above. With the exception of:
所有的步骤和前述的一样，除了:
* Download default weights file for yolov3-tiny: https://pjreddie.com/media/files/yolov3-tiny.weights
* 下载yolov3-tiny默认的权重文件https://pjreddie.com/media/files/yolov3-tiny.weights
* Get pre-trained weights `yolov3-tiny.conv.15` using command: `darknet.exe partial cfg/yolov3-tiny.cfg yolov3-tiny.weights yolov3-tiny.conv.15 15`
* 获取与训练的权重`yolov3-tiny.conv.15`,使用命令`darknet.exe partial cfg/yolov3-tiny.cfg yolov3-tiny.weights yolov3-tiny.conv.15 15`
* Make your custom model `yolov3-tiny-obj.cfg` based on `cfg/yolov3-tiny_obj.cfg` instead of `yolov3.cfg`
* 在`cfg/yolov3-tiny_obj.cfg`而不是`yolov3.cfg`的基础上创建你自己的模型`yolov3-tiny-obj.cfg`
* Start training: `darknet.exe detector train data/obj.data yolov3-tiny-obj.cfg yolov3-tiny.conv.15`
* 开始训练:`darknet.exe detector train data/obj.data yolov3-tiny-obj.cfg yolov3-tiny.conv.15`

For training Yolo based on other models ([DenseNet201-Yolo](https://github.com/AlexeyAB/darknet/blob/master/build/darknet/x64/densenet201_yolo.cfg) or [ResNet50-Yolo](https://github.com/AlexeyAB/darknet/blob/master/build/darknet/x64/resnet50_yolo.cfg)), you can download and get pre-trained weights as showed in this file: https://github.com/AlexeyAB/darknet/blob/master/build/darknet/x64/partial.cmd
基于其他模型训练YOLO([DenseNet201-Yolo](https://github.com/AlexeyAB/darknet/blob/master/build/darknet/x64/densenet201_yolo.cfg) or [ResNet50-Yolo](https://github.com/AlexeyAB/darknet/blob/master/build/darknet/x64/resnet50_yolo.cfg))，你可以下载预训练权重，像这个文件中展示的一样https://github.com/AlexeyAB/darknet/blob/master/build/darknet/x64/partial.cmd
If you made you custom model that isn't based on other models, then you can train it without pre-trained weights, then will be used random initial weights.
如果你使用自己的模型而非基于其他模型，你可以无需预训练权重，模型会随机初始化权重
 
## When should I stop training:
## 我什么时候应该停止训练

Usually sufficient 2000 iterations for each class(object), but not less than 4000 iterations in total. But for a more precise definition when you should stop training, use the following manual:
通常每一类目标2000次迭代就够了，但是总的迭代次数不能少于4000次。但若需要更精确具体一点的规则，就使用下面的手册:

1. During training, you will see varying indicators of error, and you should stop when no longer decreases **0.XXXXXXX avg**:
1. 在训练过程中，你将会看到错误指数的变化，且你应该在**0.XXXXXXX avg**不再下降的时候停止训练

  > Region Avg IOU: 0.798363, Class: 0.893232, Obj: 0.700808, No Obj: 0.004567, Avg Recall: 1.000000,  count: 8
  > Region Avg IOU: 0.800677, Class: 0.892181, Obj: 0.701590, No Obj: 0.004574, Avg Recall: 1.000000,  count: 8
  >
  > **9002**: 0.211667, **0.060730 avg**, 0.001000 rate, 3.868000 seconds, 576128 images
  > Loaded: 0.000000 seconds

  * **9002** - iteration number (number of batch)
  * **0.060730 avg** - average loss (error) - **the lower, the better**

  When you see that average loss **0.xxxxxx avg** no longer decreases at many iterations then you should stop training. The final avgerage loss can be from `0.05` (for a small model and easy dataset) to `3.0` (for a big model and a difficult dataset).
  当你看到平均损失**0.xxxxxx avg**在多次迭代后不再下降，你应该停止训练，最终的平均损失应该在0.05（小的模型，简单数据集)到3.0(大的模型和复杂数据集)之间.

2. Once training is stopped, you should take some of last `.weights`-files from `darknet\build\darknet\x64\backup` and choose the best of them:
2. 一旦训练停止，你应该从`darknet\build\darknet\x64\backup`选一些最新的`.weight`权重文件，并从中选择效果最好的。

For example, you stopped training after 9000 iterations, but the best result can give one of previous weights (7000, 8000, 9000). It can happen due to overfitting. **Overfitting** - is case when you can detect objects on images from training-dataset, but can't detect objects on any others images. You should get weights from **Early Stopping Point**:
例如，你在9000次迭代后停止了训练，但最好结果是前面迭代的权重(7000, 8000, 9000), 这在过拟合时会发生(过拟合，一种能在训练数据集中进行良好检测，而不能在其他任何图像中检测到目标的情况). 此时应该从前面的**Early Stopping Point**选择检测权重。

![Overfitting](https://hsto.org/files/5dc/7ae/7fa/5dc7ae7fad9d4e3eb3a484c58bfc1ff5.png) 

To get weights from Early Stopping Point:
为了在适止点得到权重

  2.1. At first, in your file `obj.data` you must specify the path to the validation dataset `valid = valid.txt` (format of `valid.txt` as in `train.txt`), and if you haven't validation images, just copy `data\train.txt` to `data\valid.txt`.
  2.1 首先，在你的`obj.data`文件中，你必须指定验证集的文件路径`valid = valid.txt`(格式与`train.txt`一样),如果你没有验证集，那么就拷贝`data\train.txt`到`data\valid.txt`.

  2.2 If training is stopped after 9000 iterations, to validate some of previous weights use this commands:
  2.2 如果训练在9000次迭代后停止，使用这个命令来验证一些之前的权重

(If you use another GitHub repository, then use `darknet.exe detector recall`... instead of `darknet.exe detector map`...)
(如果你使用另一个GitHub仓库，使用`darknet.exe detector recall`...而非`darknet.exe detector map`...)

* `darknet.exe detector map data/obj.data yolo-obj.cfg backup\yolo-obj_7000.weights`
* `darknet.exe detector map data/obj.data yolo-obj.cfg backup\yolo-obj_8000.weights`
* `darknet.exe detector map data/obj.data yolo-obj.cfg backup\yolo-obj_9000.weights`

And comapre last output lines for each weights (7000, 8000, 9000):
比较各个权重的输出的最后一行

Choose weights-file **with the highest mAP (mean average precision)** or IoU (intersect over union)
选择具有最高的**mAP(mean average precision)** 或者IoU的权重文件

For example, **bigger mAP** gives weights `yolo-obj_8000.weights` - then **use this weights for detection**.
例如，`yolo-obj_8000.weights`有了**更大的mAP**值,那么就使用这个权重进行检测

Or just train with `-map` flag: 
或者训练时添加`-map`参数

`darknet.exe detector train data/obj.data yolo-obj.cfg darknet53.conv.74 -map` 

So you will see mAP-chart (red-line) in the Loss-chart Window. mAP will be calculated for each 4 Epochs using `valid=valid.txt` file that is specified in `obj.data` file (`1 Epoch = images_in_train_txt / batch` iterations)
然后你将在Loss-chart窗口中看到mAP-chart(红色的线). mAP使用在`obj.data`中指定的`valid=valid.txt`文件，每4个Epochs计算一次(1 Epoch= images_in_train_txt/batch 次迭代)

![loss_chart_map_chart](https://hsto.org/webt/yd/vl/ag/ydvlagutof2zcnjodstgroen8ac.jpeg)

Example of custom object detection: `darknet.exe detector test data/obj.data yolo-obj.cfg yolo-obj_8000.weights`

* **IoU** (intersect over union) - average instersect over union of objects and detections for a certain threshold = 0.24

* **mAP** (mean average precision) - mean value of `average precisions` for each class, where `average precision` is average value of 11 points on PR-curve for each possible threshold (each probability of detection) for the same class (Precision-Recall in terms of PascalVOC, where Precision=TP/(TP+FP) and Recall=TP/(TP+FN) ), page-11: http://homepages.inf.ed.ac.uk/ckiw/postscript/ijcv_voc09.pdf

**mAP** is default metric of precision in the PascalVOC competition, **this is the same as AP50** metric in the MS COCO competition.
In terms of Wiki, indicators Precision and Recall have a slightly different meaning than in the PascalVOC competition, but **IoU always has the same meaning**.

![precision_recall_iou](https://hsto.org/files/ca8/866/d76/ca8866d76fb840228940dbf442a7f06a.jpg)

### How to calculate mAP on PascalVOC 2007:

1. To calculate mAP (mean average precision) on PascalVOC-2007-test:
* Download PascalVOC dataset, install Python 3.x and get file `2007_test.txt` as described here: https://github.com/AlexeyAB/darknet#how-to-train-pascal-voc-data
* Then download file https://raw.githubusercontent.com/AlexeyAB/darknet/master/scripts/voc_label_difficult.py to the dir `build\darknet\x64\data\` then run `voc_label_difficult.py` to get the file `difficult_2007_test.txt`
* Remove symbol `#` from this line to un-comment it: https://github.com/AlexeyAB/darknet/blob/master/build/darknet/x64/data/voc.data#L4
* Then there are 2 ways to get mAP:
    1. Using Darknet + Python: run the file `build/darknet/x64/calc_mAP_voc_py.cmd` - you will get mAP for `yolo-voc.cfg` model, mAP = 75.9%
    2. Using this fork of Darknet: run the file `build/darknet/x64/calc_mAP.cmd` - you will get mAP for `yolo-voc.cfg` model, mAP = 75.8%
    
 (The article specifies the value of mAP = 76.8% for YOLOv2 416×416, page-4 table-3: https://arxiv.org/pdf/1612.08242v1.pdf. We get values lower - perhaps due to the fact that the model was trained on a slightly different source code than the code on which the detection is was done)

* if you want to get mAP for `tiny-yolo-voc.cfg` model, then un-comment line for tiny-yolo-voc.cfg and comment line for yolo-voc.cfg in the .cmd-file
* if you have Python 2.x instead of Python 3.x, and if you use Darknet+Python-way to get mAP, then in your cmd-file use `reval_voc.py` and `voc_eval.py` instead of `reval_voc_py3.py` and `voc_eval_py3.py` from this directory: https://github.com/AlexeyAB/darknet/tree/master/scripts

### Custom object detection:

Example of custom object detection: `darknet.exe detector test data/obj.data yolo-obj.cfg yolo-obj_8000.weights`

| ![Yolo_v2_training](https://hsto.org/files/d12/1e7/515/d121e7515f6a4eb694913f10de5f2b61.jpg) | ![Yolo_v2_training](https://hsto.org/files/727/c7e/5e9/727c7e5e99bf4d4aa34027bb6a5e4bab.jpg) |
|---|---|

## How to improve object detection:

1. Before training:
  * set flag `random=1` in your `.cfg`-file - it will increase precision by training Yolo for different resolutions: [link](https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L788)

  * increase network resolution in your `.cfg`-file (`height=608`, `width=608` or any value multiple of 32) - it will increase precision


  * check that each object is mandatory labeled in your dataset - no one object in your data set should not be without label. In the most training issues - there are wrong labels in your dataset (got labels by using some conversion script, marked with a third-party tool, ...). Always check your dataset by using: https://github.com/AlexeyAB/Yolo_mark

  *  for each object which you want to detect - there must be at least 1 similar object in the Training dataset with about the same: shape, side of object, relative size, angle of rotation, tilt, illumination. So desirable that your training dataset include images with objects at diffrent: scales, rotations, lightings, from different sides, on different backgrounds - you should preferably have 2000 different images for each class or more, and you should train `2000*classes` iterations or more

  * desirable that your training dataset include images with non-labeled objects that you do not want to detect - negative samples without bounded box (empty `.txt` files) - use as many images of negative samples as there are images with objects

  * for training with a large number of objects in each image, add the parameter `max=200` or higher value in the last `[yolo]`-layer or `[region]`-layer in your cfg-file (the global maximum number of objects that can be detected by YoloV3 is `0,0615234375*(width*height)` where are width and height are parameters from `[net]` section in cfg-file) 
  
  * for training for small objects (smaller than 16x16 after the image is resized to 416x416) - set `layers = -1, 11` instead of https://github.com/AlexeyAB/darknet/blob/6390a5a2ab61a0bdf6f1a9a6b4a739c16b36e0d7/cfg/yolov3.cfg#L720
      and set `stride=4` instead of https://github.com/AlexeyAB/darknet/blob/6390a5a2ab61a0bdf6f1a9a6b4a739c16b36e0d7/cfg/yolov3.cfg#L717
  
  * for training for both small and large objects use modified models:
      * Full-model: 5 yolo layers: https://raw.githubusercontent.com/AlexeyAB/darknet/master/cfg/yolov3_5l.cfg
      * Tiny-model: 3 yolo layers: https://raw.githubusercontent.com/AlexeyAB/darknet/master/cfg/yolov3-tiny_3l.cfg
      * Spatial-full-model: 3 yolo layers: https://raw.githubusercontent.com/AlexeyAB/darknet/master/cfg/yolov3-spp.cfg
  
  * If you train the model to distinguish Left and Right objects as separate classes (left/right hand, left/right-turn on road signs, ...) then for disabling flip data augmentation - add `flip=0` here: https://github.com/AlexeyAB/darknet/blob/3d2d0a7c98dbc8923d9ff705b81ff4f7940ea6ff/cfg/yolov3.cfg#L17
  
  * General rule - your training dataset should include such a set of relative sizes of objects that you want to detect: 

    * `train_network_width * train_obj_width / train_image_width ~= detection_network_width * detection_obj_width / detection_image_width`
    * `train_network_height * train_obj_height / train_image_height ~= detection_network_height * detection_obj_height / detection_image_height`
    
    I.e. for each object from Test dataset there must be at least 1 object in the Training dataset with the same class_id and about the same relative size:

    `object width in percent from Training dataset` ~= `object width in percent from Test dataset` 
   
    That is, if only objects that occupied 80-90% of the image were present in the training set, then the trained network will not be able to detect objects that occupy 1-10% of the image.
    
  * to speedup training (with decreasing detection accuracy) do Fine-Tuning instead of Transfer-Learning, set param `stopbackward=1` here: https://github.com/AlexeyAB/darknet/blob/6d44529cf93211c319813c90e0c1adb34426abe5/cfg/yolov3.cfg#L548
    then do this command: `./darknet partial cfg/yolov3.cfg yolov3.weights yolov3.conv.81 81` will be created file `yolov3.conv.81`,
    then train by using weights file `yolov3.conv.81` instead of `darknet53.conv.74`

  * each: `model of object, side, illimination, scale, each 30 grad` of the turn and inclination angles - these are *different objects* from an internal perspective of the neural network. So the more *different objects* you want to detect, the more complex network model should be used.

  * recalculate anchors for your dataset for `width` and `height` from cfg-file:
  `darknet.exe detector calc_anchors data/obj.data -num_of_clusters 9 -width 416 -height 416`
   then set the same 9 `anchors` in each of 3 `[yolo]`-layers in your cfg-file. But you should change indexes of anchors `masks=` for each [yolo]-layer, so that 1st-[yolo]-layer has anchors larger than 60x60, 2nd larger than 30x30, 3rd remaining. Also you should change the `filters=(classes + 5)*<number of mask>` before each [yolo]-layer. If many of the calculated anchors do not fit under the appropriate layers - then just try using all the default anchors.


2. After training - for detection:

  * Increase network-resolution by set in your `.cfg`-file (`height=608` and `width=608`) or (`height=832` and `width=832`) or (any value multiple of 32) - this increases the precision and makes it possible to detect small objects: [link](https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L8-L9)
  
    * it is not necessary to train the network again, just use `.weights`-file already trained for 416x416 resolution
    * but to get even greater accuracy you should train with higher resolution 608x608 or 832x832, note: if error `Out of memory` occurs then in `.cfg`-file you should increase `subdivisions=16`, 32 or 64: [link](https://github.com/AlexeyAB/darknet/blob/0039fd26786ab5f71d5af725fc18b3f521e7acfd/cfg/yolov3.cfg#L4)

## How to mark bounded boxes of objects and create annotation files:

Here you can find repository with GUI-software for marking bounded boxes of objects and generating annotation files for Yolo v2 & v3: https://github.com/AlexeyAB/Yolo_mark

With example of: `train.txt`, `obj.names`, `obj.data`, `yolo-obj.cfg`, `air`1-6`.txt`, `bird`1-4`.txt` for 2 classes of objects (air, bird) and `train_obj.cmd` with example how to train this image-set with Yolo v2 & v3

## Using Yolo9000

 Simultaneous detection and classification of 9000 objects: `darknet.exe detector test cfg/combine9k.data cfg/yolo9000.cfg yolo9000.weights data/dog.jpg`

* `yolo9000.weights` - (186 MB Yolo9000 Model) requires 4 GB GPU-RAM: http://pjreddie.com/media/files/yolo9000.weights

* `yolo9000.cfg` - cfg-file of the Yolo9000, also there are paths to the `9k.tree` and `coco9k.map`  https://github.com/AlexeyAB/darknet/blob/617cf313ccb1fe005db3f7d88dec04a04bd97cc2/cfg/yolo9000.cfg#L217-L218

    * `9k.tree` - **WordTree** of 9418 categories  - `<label> <parent_it>`, if `parent_id == -1` then this label hasn't parent: https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/9k.tree

    * `coco9k.map` - map 80 categories from MSCOCO to WordTree `9k.tree`: https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/coco9k.map

* `combine9k.data` - data file, there are paths to: `9k.labels`, `9k.names`, `inet9k.map`, (change path to your `combine9k.train.list`): https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/combine9k.data

    * `9k.labels` - 9418 labels of objects: https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/9k.labels

    * `9k.names` -
9418 names of objects: https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/9k.names

    * `inet9k.map` - map 200 categories from ImageNet to WordTree `9k.tree`: https://raw.githubusercontent.com/AlexeyAB/darknet/master/build/darknet/x64/data/inet9k.map


## How to use Yolo as DLL and SO libraries
## 如何将YOLO作为动态链接库使用

* on Linux - set `LIBSO=1` in the `Makefile` and do `make`
* 在Linux上 - 在`Makefile`中设置`LIBSO=1`然后`make`
* on Windows - compile `build\darknet\yolo_cpp_dll.sln` or `build\darknet\yolo_cpp_dll_no_gpu.sln` solution
* 在Windows上 - 编译`build\darknet\yolo_cpp_dll.sln`或者`build\darknet\yolo_cpp_dll_no_gpu.sln`这两个解决方案

There are 2 APIs:
这里提供两个API:
* C API: https://github.com/AlexeyAB/darknet/blob/master/include/darknet.h
    * Python examples using the C API::     
         * https://github.com/AlexeyAB/darknet/blob/master/darknet.py	
         * https://github.com/AlexeyAB/darknet/blob/master/darknet_video.py
* C API: https://github.com/AlexeyAB/darknet/blob/master/include/darknet.h
    * Python使用 C API示例::
         * https://github.com/AlexeyAB/darknet/blob/master/darknet.py	
         * https://github.com/AlexeyAB/darknet/blob/master/darknet_video.py
    
* C++ API: https://github.com/AlexeyAB/darknet/blob/master/include/yolo_v2_class.hpp
    * C++ example that uses C++ API: https://github.com/AlexeyAB/darknet/blob/master/src/yolo_console_dll.cpp
* C++ API: https://github.com/AlexeyAB/darknet/blob/master/include/yolo_v2_class.hpp
    * C++ 使用示例: https://github.com/AlexeyAB/darknet/blob/master/src/yolo_console_dll.cpp
----

1. To compile Yolo as C++ DLL-file `yolo_cpp_dll.dll` - open in MSVS2015 file `build\darknet\yolo_cpp_dll.sln`, set **x64** and **Release**, and do the: Build -> Build yolo_cpp_dll
    * You should have installed **CUDA 10.0**
    * To use cuDNN do: (right click on project) -> properties -> C/C++ -> Preprocessor -> Preprocessor Definitions, and add at the beginning of line: `CUDNN;`

2. To use Yolo as DLL-file in your C++ console application - open in MSVS2015 file `build\darknet\yolo_console_dll.sln`, set **x64** and **Release**, and do the: Build -> Build yolo_console_dll

    * you can run your console application from Windows Explorer `build\darknet\x64\yolo_console_dll.exe`
    **use this command**: `yolo_console_dll.exe data/coco.names yolov3.cfg yolov3.weights test.mp4`
    
    * after launching your console application and entering the image file name - you will see info for each object: 
    `<obj_id> <left_x> <top_y> <width> <height> <probability>`
    * to use simple OpenCV-GUI you should uncomment line `//#define OPENCV` in `yolo_console_dll.cpp`-file: [link](https://github.com/AlexeyAB/darknet/blob/a6cbaeecde40f91ddc3ea09aa26a03ab5bbf8ba8/src/yolo_console_dll.cpp#L5)
    * you can see source code of simple example for detection on the video file: [link](https://github.com/AlexeyAB/darknet/blob/ab1c5f9e57b4175f29a6ef39e7e68987d3e98704/src/yolo_console_dll.cpp#L75)
   
`yolo_cpp_dll.dll`-API: [link](https://github.com/AlexeyAB/darknet/blob/master/src/yolo_v2_class.hpp#L42)
```
struct bbox_t {
    unsigned int x, y, w, h;    // (x,y) - top-left corner, (w, h) - width & height of bounded box
    float prob;                    // confidence - probability that the object was found correctly
    unsigned int obj_id;        // class of object - from range [0, classes-1]
    unsigned int track_id;        // tracking id for video (0 - untracked, 1 - inf - tracked object)
    unsigned int frames_counter;// counter of frames on which the object was detected
};

class Detector {
public:
        Detector(std::string cfg_filename, std::string weight_filename, int gpu_id = 0);
        ~Detector();

        std::vector<bbox_t> detect(std::string image_filename, float thresh = 0.2, bool use_mean = false);
        std::vector<bbox_t> detect(image_t img, float thresh = 0.2, bool use_mean = false);
        static image_t load_image(std::string image_filename);
        static void free_image(image_t m);

#ifdef OPENCV
        std::vector<bbox_t> detect(cv::Mat mat, float thresh = 0.2, bool use_mean = false);
	std::shared_ptr<image_t> mat_to_image_resize(cv::Mat mat) const;
#endif
};
```
