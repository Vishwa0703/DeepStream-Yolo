# DeepStream-Yolo

NVIDIA DeepStream SDK 6.2 / 6.1.1 / 6.1 / 6.0.1 / 6.0 configuration for YOLO models

-------------------------------------
### **Big update on DeepStream-Yolo**
-------------------------------------
### Important: please generate the ONNX model and the TensorRT engine again with the updated files
-------------------------------------

### Future updates

* DeepStream tutorials
* Dynamic batch-size
* Updated INT8 calibration
* Support for segmentation models
* Support for classification models

### Improvements on this repository

* Support for INT8 calibration
* Support for non square models
* Models benchmarks
* **Support for Darknet YOLO models (YOLOv4, etc) using cfg and weights conversion with GPU post-processing**
* **Support for YOLO-NAS, PPYOLOE+, PPYOLOE, DAMO-YOLO, YOLOX, YOLOR, YOLOv8, YOLOv7, YOLOv6 and YOLOv5 using ONNX conversion with GPU post-processing**
* **Add GPU bbox parser (it is slightly slower than CPU bbox parser on V100 GPU tests)**

##

### Getting started

* [Requirements](#requirements)
* [Suported models](#supported-models)
* [Benchmarks](#benchmarks)
* [dGPU installation](#dgpu-installation)
* [Basic usage](#basic-usage)
* [Docker usage](#docker-usage)
* [NMS configuration](#nms-configuration)
* [INT8 calibration](#int8-calibration)
* [YOLOv5 usage](docs/YOLOv5.md)
* [YOLOv6 usage](docs/YOLOv6.md)
* [YOLOv7 usage](docs/YOLOv7.md)
* [YOLOv8 usage](docs/YOLOv8.md)
* [YOLOR usage](docs/YOLOR.md)
* [YOLOX usage](docs/YOLOX.md)
* [DAMO-YOLO usage](docs/DAMOYOLO.md)
* [PP-YOLOE / PP-YOLOE+ usage](docs/PPYOLOE.md)
* [YOLO-NAS usage](docs/YOLONAS.md)
* [Using your custom model](docs/customModels.md)
* [Multiple YOLO GIEs](docs/multipleGIEs.md)

##

### Requirements

#### DeepStream 6.2 on x86 platform

* [Ubuntu 20.04](https://releases.ubuntu.com/20.04/)
* [CUDA 11.8](https://developer.nvidia.com/cuda-11-8-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=runfile_local)
* [TensorRT 8.5 GA Update 1 (8.5.2.2)](https://developer.nvidia.com/nvidia-tensorrt-8x-download)
* [NVIDIA Driver 525.85.12 (Data center / Tesla series) / 525.105.17 (TITAN, GeForce RTX / GTX series and RTX / Quadro series)](https://www.nvidia.com.br/Download/index.aspx)
* [NVIDIA DeepStream SDK 6.2](https://developer.nvidia.com/deepstream-getting-started)
* [GStreamer 1.16.3](https://gstreamer.freedesktop.org/)
* [DeepStream-Yolo](https://github.com/marcoslucianops/DeepStream-Yolo)

#### DeepStream 6.1.1 on x86 platform

* [Ubuntu 20.04](https://releases.ubuntu.com/20.04/)
* [CUDA 11.7 Update 1](https://developer.nvidia.com/cuda-11-7-1-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=runfile_local)
* [TensorRT 8.4 GA (8.4.1.5)](https://developer.nvidia.com/nvidia-tensorrt-8x-download)
* [NVIDIA Driver 515.65.01](https://www.nvidia.com.br/Download/index.aspx)
* [NVIDIA DeepStream SDK 6.1.1](https://developer.nvidia.com/deepstream-sdk-download-tesla-archived)
* [GStreamer 1.16.2](https://gstreamer.freedesktop.org/)
* [DeepStream-Yolo](https://github.com/marcoslucianops/DeepStream-Yolo)

#### DeepStream 6.1 on x86 platform

* [Ubuntu 20.04](https://releases.ubuntu.com/20.04/)
* [CUDA 11.6 Update 1](https://developer.nvidia.com/cuda-11-6-1-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=runfile_local)
* [TensorRT 8.2 GA Update 4 (8.2.5.1)](https://developer.nvidia.com/nvidia-tensorrt-8x-download)
* [NVIDIA Driver 510.47.03](https://www.nvidia.com.br/Download/index.aspx)
* [NVIDIA DeepStream SDK 6.1](https://developer.nvidia.com/deepstream-sdk-download-tesla-archived)
* [GStreamer 1.16.2](https://gstreamer.freedesktop.org/)
* [DeepStream-Yolo](https://github.com/marcoslucianops/DeepStream-Yolo)

#### DeepStream 6.0.1 / 6.0 on x86 platform

* [Ubuntu 18.04](https://releases.ubuntu.com/18.04.6/)
* [CUDA 11.4 Update 1](https://developer.nvidia.com/cuda-11-4-1-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=18.04&target_type=runfile_local)
* [TensorRT 8.0 GA (8.0.1)](https://developer.nvidia.com/nvidia-tensorrt-8x-download)
* [NVIDIA Driver 470.63.01](https://www.nvidia.com.br/Download/index.aspx)
* [NVIDIA DeepStream SDK 6.0.1 / 6.0](https://developer.nvidia.com/deepstream-sdk-download-tesla-archived)
* [GStreamer 1.14.5](https://gstreamer.freedesktop.org/)
* [DeepStream-Yolo](https://github.com/marcoslucianops/DeepStream-Yolo)

#### DeepStream 6.2 on Jetson platform

* [JetPack 5.1.1 / 5.1](https://developer.nvidia.com/embedded/jetpack)
* [NVIDIA DeepStream SDK 6.2](https://developer.nvidia.com/deepstream-sdk)
* [DeepStream-Yolo](https://github.com/marcoslucianops/DeepStream-Yolo)

#### DeepStream 6.1.1 on Jetson platform

* [JetPack 5.0.2](https://developer.nvidia.com/embedded/jetpack-sdk-502)
* [NVIDIA DeepStream SDK 6.1.1](https://developer.nvidia.com/embedded/deepstream-on-jetson-downloads-archived)
* [DeepStream-Yolo](https://github.com/marcoslucianops/DeepStream-Yolo)

#### DeepStream 6.1 on Jetson platform

* [JetPack 5.0.1 DP](https://developer.nvidia.com/embedded/jetpack-sdk-501dp)
* [NVIDIA DeepStream SDK 6.1](https://developer.nvidia.com/embedded/deepstream-on-jetson-downloads-archived)
* [DeepStream-Yolo](https://github.com/marcoslucianops/DeepStream-Yolo)

#### DeepStream 6.0.1 / 6.0 on Jetson platform

* [JetPack 4.6.2](https://developer.nvidia.com/embedded/jetpack-sdk-462)
* [NVIDIA DeepStream SDK 6.0.1 / 6.0](https://developer.nvidia.com/embedded/deepstream-on-jetson-downloads-archived)
* [DeepStream-Yolo](https://github.com/marcoslucianops/DeepStream-Yolo)

##

### Suported models

* [Darknet YOLO](https://github.com/AlexeyAB/darknet)
* [MobileNet-YOLO](https://github.com/dog-qiuqiu/MobileNet-Yolo)
* [YOLO-Fastest](https://github.com/dog-qiuqiu/Yolo-Fastest)
* [YOLOv5](https://github.com/ultralytics/yolov5)
* [YOLOv6](https://github.com/meituan/YOLOv6)
* [YOLOv7](https://github.com/WongKinYiu/yolov7)
* [YOLOv8](https://github.com/ultralytics/ultralytics)
* [YOLOR](https://github.com/WongKinYiu/yolor)
* [YOLOX](https://github.com/Megvii-BaseDetection/YOLOX)
* [DAMO-YOLO](https://github.com/tinyvision/DAMO-YOLO)
* [PP-YOLOE / PP-YOLOE+](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.6/configs/ppyoloe)
* [YOLO-NAS](https://github.com/Deci-AI/super-gradients/blob/master/YOLONAS.md)

##

### Benchmarks

#### Config

```
board = NVIDIA Tesla V100 16GB (AWS: p3.2xlarge)
batch-size = 1
eval = val2017 (COCO)
sample = 1920x1080 video
```

**NOTE**: Used maintain-aspect-ratio=1 in config_infer file for Darknet (with letter_box=1) and PyTorch models.

#### NMS config

- Eval

```
nms-iou-threshold = 0.6 (Darknet) / 0.65 (YOLOv5, YOLOv6, YOLOv7, YOLOR and YOLOX) / 0.7 (Paddle, YOLO-NAS, DAMO-YOLO, YOLOv8 and YOLOv7-u6)
pre-cluster-threshold = 0.001
topk = 300
```

- Test

```
nms-iou-threshold = 0.45
pre-cluster-threshold = 0.25
topk = 300
```

#### Results

**NOTE**: * = PyTorch.

**NOTE**: ** = The YOLOv4 is trained with the trainvalno5k set, so the mAP is high on val2017 test.

**NOTE**: star = DAMO-YOLO model trained with distillation.

**NOTE**: The V100 GPU decoder max out at 625-635 FPS on DeepStream even using lighter models.

**NOTE**: The GPU bbox parser is a bit slower than CPU bbox parser on V100 GPU tests.

| DeepStream         | Precision | Resolution | IoU=0.5:0.95 | IoU=0.5 | IoU=0.75 | FPS<br />(without display) |
|:------------------:|:---------:|:----------:|:------------:|:-------:|:--------:|:--------------------------:|
| YOLO-NAS L         | FP16      | 640        | 0.484        | 0.658   | 0.532    | 235.27                     |
| YOLO-NAS M         | FP16      | 640        | 0.480        | 0.651   | 0.524    | 287.39                     |
| YOLO-NAS S         | FP16      | 640        | 0.442        | 0.614   | 0.485    | 478.52                     |
| PP-YOLOE+_x        | FP16      | 640        | 0.528        | 0.705   | 0.579    | 121.17                     |
| PP-YOLOE+_l        | FP16      | 640        | 0.511        | 0.686   | 0.557    | 191.82                     |
| PP-YOLOE+_m        | FP16      | 640        | 0.483        | 0.658   | 0.528    | 264.39                     |
| PP-YOLOE+_s        | FP16      | 640        | 0.424        | 0.594   | 0.464    | 476.13                     |
| PP-YOLOE-s (400)   | FP16      | 640        | 0.423        | 0.589   | 0.463    | 461.23                     |
| DAMO-YOLO-L star   | FP16      | 640        | 0.502        | 0.674   | 0.551    | 176.93                     |
| DAMO-YOLO-M star   | FP16      | 640        | 0.485        | 0.656   | 0.530    | 242.24                     |
| DAMO-YOLO-S star   | FP16      | 640        | 0.460        | 0.631   | 0.502    | 385.09                     |
| DAMO-YOLO-S        | FP16      | 640        | 0.445        | 0.611   | 0.486    | 378.68                     |
| DAMO-YOLO-T star   | FP16      | 640        | 0.419        | 0.586   | 0.455    | 492.24                     |
| DAMO-YOLO-Nl       | FP16      | 416        | 0.392        | 0.559   | 0.423    | 483.73                     |
| DAMO-YOLO-Nm       | FP16      | 416        | 0.371        | 0.532   | 0.402    | 555.94                     |
| DAMO-YOLO-Ns       | FP16      | 416        | 0.312        | 0.460   | 0.335    | 627.67                     |
| YOLOX-x            | FP16      | 640        | 0.447        | 0.616   | 0.483    | 125.40                     |
| YOLOX-l            | FP16      | 640        | 0.430        | 0.598   | 0.466    | 193.10                     |
| YOLOX-m            | FP16      | 640        | 0.397        | 0.566   | 0.431    | 298.61                     |
| YOLOX-s            | FP16      | 640        | 0.335        | 0.502   | 0.365    | 522.05                     |
| YOLOX-s legacy     | FP16      | 640        | 0.375        | 0.569   | 0.407    | 518.52                     |
| YOLOX-Darknet      | FP16      | 640        | 0.414        | 0.595   | 0.453    | 212.88                     |
| YOLOX-Tiny         | FP16      | 640        | 0.274        | 0.427   | 0.292    | 633.95                     |
| YOLOX-Nano         | FP16      | 640        | 0.212        | 0.342   | 0.222    | 633.04                     |
| YOLOv8x            | FP16      | 640        | 0.499        | 0.669   | 0.545    | 130.49                     |
| YOLOv8l            | FP16      | 640        | 0.491        | 0.660   | 0.535    | 180.75                     |
| YOLOv8m            | FP16      | 640        | 0.468        | 0.637   | 0.510    | 278.08                     |
| YOLOv8s            | FP16      | 640        | 0.415        | 0.578   | 0.453    | 493.45                     |
| YOLOv8n            | FP16      | 640        | 0.343        | 0.492   | 0.373    | 627.43                     |
| YOLOv7-u6          | FP16      | 640        | 0.484        | 0.652   | 0.530    | 193.54                     |
| YOLOv7x*           | FP16      | 640        | 0.496        | 0.679   | 0.536    | 155.07                     |
| YOLOv7*            | FP16      | 640        | 0.476        | 0.660   | 0.518    | 226.01                     |
| YOLOv7-Tiny Leaky* | FP16      | 640        | 0.345        | 0.516   | 0.372    | 626.23                     |
| YOLOv7-Tiny Leaky* | FP16      | 416        | 0.328        | 0.493   | 0.349    | 633.90                     |
| YOLOv6-L 4.0       | FP16      | 640        | 0.490        | 0.671   | 0.535    | 178.41                     |
| YOLOv6-M 4.0       | FP16      | 640        | 0.460        | 0.635   | 0.502    | 293.39                     |
| YOLOv6-S 4.0       | FP16      | 640        | 0.416        | 0.585   | 0.453    | 513.90                     |
| YOLOv6-N 4.0       | FP16      | 640        | 0.349        | 0.503   | 0.378    | 633.37                     |
| YOLOv5x 7.0        | FP16      | 640        | 0.471        | 0.652   | 0.513    | 149.93                     |
| YOLOv5l 7.0        | FP16      | 640        | 0.455        | 0.637   | 0.497    | 235.55                     |
| YOLOv5m 7.0        | FP16      | 640        | 0.421        | 0.604   | 0.459    | 351.69                     |
| YOLOv5s 7.0        | FP16      | 640        | 0.344        | 0.529   | 0.372    | 618.13                     |
| YOLOv5n 7.0        | FP16      | 640        | 0.247        | 0.414   | 0.257    | 629.66                     |

##

### dGPU installation

To install the DeepStream on dGPU (x86 platform), without docker, we need to do some steps to prepare the computer.

<details><summary>DeepStream 6.2</summary>

#### 1. Disable Secure Boot in BIOS

#### 2. Install dependencies

```
sudo apt-get update
sudo apt-get install gcc make git libtool autoconf autogen pkg-config cmake
sudo apt-get install python3 python3-dev python3-pip
sudo apt-get install dkms
sudo apt install libssl1.1 libgstreamer1.0-0 gstreamer1.0-tools gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav libgstreamer-plugins-base1.0-dev libgstrtspserver-1.0-0 libjansson4 libyaml-cpp-dev libjsoncpp-dev protobuf-compiler
sudo apt-get install linux-headers-$(uname -r)
```

**NOTE**: Purge all NVIDIA driver, CUDA, etc (replace $CUDA_PATH to your CUDA path)

```
sudo nvidia-uninstall
sudo $CUDA_PATH/bin/cuda-uninstaller
sudo apt-get remove --purge '*nvidia*'
sudo apt-get remove --purge '*cuda*'
sudo apt-get remove --purge '*cudnn*'
sudo apt-get remove --purge '*tensorrt*'
sudo apt autoremove --purge && sudo apt autoclean && sudo apt clean
```

#### 3. Install CUDA Keyring

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt-get update
```

#### 4. Download and install NVIDIA Driver

<details><summary>TITAN, GeForce RTX / GTX series and RTX / Quadro series</summary><blockquote>

- Download

  ```
  wget https://us.download.nvidia.com/XFree86/Linux-x86_64/525.105.17/NVIDIA-Linux-x86_64-525.105.17.run
  ```

<blockquote><details><summary>Laptop</summary>

* Run

  ```
  sudo sh NVIDIA-Linux-x86_64-525.105.17.run --no-cc-version-check --silent --disable-nouveau --dkms --install-libglvnd
  ```

  **NOTE**: This step will disable the nouveau drivers.

* Reboot

  ```
  sudo reboot
  ```

* Install

  ```
  sudo sh NVIDIA-Linux-x86_64-525.105.17.run --no-cc-version-check --silent --disable-nouveau --dkms --install-libglvnd
  ```

**NOTE**: If you are using a laptop with NVIDIA Optimius, run

```
sudo apt-get install nvidia-prime
sudo prime-select nvidia
```

</details></blockquote>

<blockquote><details><summary>Desktop</summary>

* Run

  ```
  sudo sh NVIDIA-Linux-x86_64-525.105.17.run --no-cc-version-check --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
  ```

  **NOTE**: This step will disable the nouveau drivers.

* Reboot

  ```
  sudo reboot
  ```

* Install

  ```
  sudo sh NVIDIA-Linux-x86_64-525.105.17.run --no-cc-version-check --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
  ```

</details></blockquote>

</blockquote></details>

<details><summary>Data center / Tesla series</summary><blockquote>

  - Download

    ```
    wget https://us.download.nvidia.com/XFree86/Linux-x86_64/525.105.17/NVIDIA-Linux-x86_64-525.105.17.run
    ```

  * Run

    ```
    sudo sh NVIDIA-Linux-x86_64-525.105.17.run --no-cc-version-check --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
    ```

</blockquote></details>

#### 5. Download and install CUDA

```
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda_11.8.0_520.61.05_linux.run
sudo sh cuda_11.8.0_520.61.05_linux.run --silent --toolkit
```

* Export environment variables

  ```
  echo $'export PATH=/usr/local/cuda-11.8/bin${PATH:+:${PATH}}\nexport LD_LIBRARY_PATH=/usr/local/cuda-11.8/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}' >> ~/.bashrc && source ~/.bashrc
  ```

#### 6. Install TensorRT

```
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/3bf863cc.pub
sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /"
sudo apt-get update
sudo apt-get install libnvinfer8=8.5.2-1+cuda11.8 libnvinfer-plugin8=8.5.2-1+cuda11.8 libnvparsers8=8.5.2-1+cuda11.8 libnvonnxparsers8=8.5.2-1+cuda11.8 libnvinfer-bin=8.5.2-1+cuda11.8 libnvinfer-dev=8.5.2-1+cuda11.8 libnvinfer-plugin-dev=8.5.2-1+cuda11.8 libnvparsers-dev=8.5.2-1+cuda11.8 libnvonnxparsers-dev=8.5.2-1+cuda11.8 libnvinfer-samples=8.5.2-1+cuda11.8 libcudnn8=8.7.0.84-1+cuda11.8 libcudnn8-dev=8.7.0.84-1+cuda11.8 python3-libnvinfer=8.5.2-1+cuda11.8 python3-libnvinfer-dev=8.5.2-1+cuda11.8
sudo apt-mark hold libnvinfer* libnvparsers* libnvonnxparsers* libcudnn8* python3-libnvinfer* tensorrt
```

#### 7. Download from [NVIDIA website](https://developer.nvidia.com/deepstream-getting-started) and install the DeepStream SDK

DeepStream 6.2 for Servers and Workstations (.deb)

```
sudo apt-get install ./deepstream-6.2_6.2.0-1_amd64.deb
rm ${HOME}/.cache/gstreamer-1.0/registry.x86_64.bin
sudo ln -snf /usr/local/cuda-11.8 /usr/local/cuda
```

#### 8. Reboot the computer

```
sudo reboot
```

</details>

<details><summary>DeepStream 6.1.1</summary>

#### 1. Disable Secure Boot in BIOS

#### 2. Install dependencies

```
sudo apt-get update
sudo apt-get install gcc make git libtool autoconf autogen pkg-config cmake
sudo apt-get install python3 python3-dev python3-pip
sudo apt-get install dkms
sudo apt-get install libssl1.1 libgstreamer1.0-0 gstreamer1.0-tools gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav libgstreamer-plugins-base1.0-dev libgstrtspserver-1.0-0 libjansson4 libyaml-cpp-dev
sudo apt-get install linux-headers-$(uname -r)
```

**NOTE**: Purge all NVIDIA driver, CUDA, etc (replace $CUDA_PATH to your CUDA path)

```
sudo nvidia-uninstall
sudo $CUDA_PATH/bin/cuda-uninstaller
sudo apt-get remove --purge '*nvidia*'
sudo apt-get remove --purge '*cuda*'
sudo apt-get remove --purge '*cudnn*'
sudo apt-get remove --purge '*tensorrt*'
sudo apt autoremove --purge && sudo apt autoclean && sudo apt clean
```

#### 3. Install CUDA Keyring

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt-get update
```

#### 4. Download and install NVIDIA Driver

<details><summary>TITAN, GeForce RTX / GTX series and RTX / Quadro series</summary><blockquote>

- Download

  ```
  wget https://us.download.nvidia.com/XFree86/Linux-x86_64/515.65.01/NVIDIA-Linux-x86_64-515.65.01.run
  ```

<blockquote><details><summary>Laptop</summary>

* Run

  ```
  sudo sh NVIDIA-Linux-x86_64-515.65.01.run --silent --disable-nouveau --dkms --install-libglvnd
  ```

  **NOTE**: This step will disable the nouveau drivers.

* Reboot

  ```
  sudo reboot
  ```

* Install

  ```
  sudo sh NVIDIA-Linux-x86_64-515.65.01.run --silent --disable-nouveau --dkms --install-libglvnd
  ```

**NOTE**: If you are using a laptop with NVIDIA Optimius, run

```
sudo apt-get install nvidia-prime
sudo prime-select nvidia
```

</details></blockquote>

<blockquote><details><summary>Desktop</summary>

* Run

  ```
  sudo sh NVIDIA-Linux-x86_64-515.65.01.run --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
  ```

  **NOTE**: This step will disable the nouveau drivers.

* Reboot

  ```
  sudo reboot
  ```

* Install

  ```
  sudo sh NVIDIA-Linux-x86_64-515.65.01.run --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
  ```

</details></blockquote>

</blockquote></details>

<details><summary>Data center / Tesla series</summary><blockquote>

  - Download

    ```
    wget https://us.download.nvidia.com/tesla/515.65.01/NVIDIA-Linux-x86_64-515.65.01.run
    ```

  * Run

    ```
    sudo sh NVIDIA-Linux-x86_64-515.65.01.run --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
    ```

</blockquote></details>

#### 5. Download and install CUDA

```
wget https://developer.download.nvidia.com/compute/cuda/11.7.1/local_installers/cuda_11.7.1_515.65.01_linux.run
sudo sh cuda_11.7.1_515.65.01_linux.run --silent --toolkit
```

* Export environment variables

  ```
  echo $'export PATH=/usr/local/cuda-11.7/bin${PATH:+:${PATH}}\nexport LD_LIBRARY_PATH=/usr/local/cuda-11.7/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}' >> ~/.bashrc && source ~/.bashrc
  ```

#### 6. Download from [NVIDIA website](https://developer.nvidia.com/nvidia-tensorrt-8x-download) and install the TensorRT

TensorRT 8.4 GA for Ubuntu 20.04 and CUDA 11.0, 11.1, 11.2, 11.3, 11.4, 11.5, 11.6 and 11.7 DEB local repo Package

```
sudo dpkg -i nv-tensorrt-repo-ubuntu2004-cuda11.6-trt8.4.1.5-ga-20220604_1-1_amd64.deb 
sudo apt-key add /var/nv-tensorrt-repo-ubuntu2004-cuda11.6-trt8.4.1.5-ga-20220604/9a60d8bf.pub
sudo apt-get update
sudo apt-get install libnvinfer8=8.4.1-1+cuda11.6 libnvinfer-plugin8=8.4.1-1+cuda11.6 libnvparsers8=8.4.1-1+cuda11.6 libnvonnxparsers8=8.4.1-1+cuda11.6 libnvinfer-bin=8.4.1-1+cuda11.6 libnvinfer-dev=8.4.1-1+cuda11.6 libnvinfer-plugin-dev=8.4.1-1+cuda11.6 libnvparsers-dev=8.4.1-1+cuda11.6 libnvonnxparsers-dev=8.4.1-1+cuda11.6 libnvinfer-samples=8.4.1-1+cuda11.6 libcudnn8=8.4.1.50-1+cuda11.6 libcudnn8-dev=8.4.1.50-1+cuda11.6 python3-libnvinfer=8.4.1-1+cuda11.6 python3-libnvinfer-dev=8.4.1-1+cuda11.6
sudo apt-mark hold libnvinfer* libnvparsers* libnvonnxparsers* libcudnn8* tensorrt
```

#### 7. Download from [NVIDIA website](https://developer.nvidia.com/deepstream-getting-started) and install the DeepStream SDK

DeepStream 6.1.1 for Servers and Workstations (.deb)

```
sudo apt-get install ./deepstream-6.1_6.1.1-1_amd64.deb
rm ${HOME}/.cache/gstreamer-1.0/registry.x86_64.bin
sudo ln -snf /usr/local/cuda-11.7 /usr/local/cuda
```

#### 8. Reboot the computer

```
sudo reboot
```

</details>

<details><summary>DeepStream 6.1</summary>

#### 1. Disable Secure Boot in BIOS

#### 2. Install dependencies

```
sudo apt-get update
sudo apt-get install gcc make git libtool autoconf autogen pkg-config cmake
sudo apt-get install python3 python3-dev python3-pip
sudo apt-get install dkms
sudo apt-get install libssl1.1 libgstreamer1.0-0 gstreamer1.0-tools gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav libgstrtspserver-1.0-0 libjansson4 libyaml-cpp-dev
sudo apt-get install linux-headers-$(uname -r)
```

**NOTE**: Purge all NVIDIA driver, CUDA, etc (replace $CUDA_PATH to your CUDA path)

```
sudo nvidia-uninstall
sudo $CUDA_PATH/bin/cuda-uninstaller
sudo apt-get remove --purge '*nvidia*'
sudo apt-get remove --purge '*cuda*'
sudo apt-get remove --purge '*cudnn*'
sudo apt-get remove --purge '*tensorrt*'
sudo apt autoremove --purge && sudo apt autoclean && sudo apt clean
```

#### 3. Install CUDA Keyring

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt-get update
```

#### 4. Download and install NVIDIA Driver

<details><summary>TITAN, GeForce RTX / GTX series and RTX / Quadro series</summary><blockquote>

- Download

  ```
  wget https://us.download.nvidia.com/XFree86/Linux-x86_64/510.47.03/NVIDIA-Linux-x86_64-510.47.03.run
  ```

<blockquote><details><summary>Laptop</summary>

* Run

  ```
  sudo sh NVIDIA-Linux-x86_64-510.47.03.run --silent --disable-nouveau --dkms --install-libglvnd
  ```

  **NOTE**: This step will disable the nouveau drivers.

* Reboot

  ```
  sudo reboot
  ```

* Install

  ```
  sudo sh NVIDIA-Linux-x86_64-510.47.03.run --silent --disable-nouveau --dkms --install-libglvnd
  ```

**NOTE**: If you are using a laptop with NVIDIA Optimius, run

```
sudo apt-get install nvidia-prime
sudo prime-select nvidia
```

</details></blockquote>

<blockquote><details><summary>Desktop</summary>

* Run

  ```
  sudo sh NVIDIA-Linux-x86_64-510.47.03.run --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
  ```

  **NOTE**: This step will disable the nouveau drivers.

* Reboot

  ```
  sudo reboot
  ```

* Install

  ```
  sudo sh NVIDIA-Linux-x86_64-510.47.03.run --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
  ```

</details></blockquote>

</blockquote></details>

<details><summary>Data center / Tesla series</summary><blockquote>

  - Download

    ```
    wget https://us.download.nvidia.com/tesla/510.47.03/NVIDIA-Linux-x86_64-510.47.03.run
    ```

  * Run

    ```
    sudo sh NVIDIA-Linux-x86_64-510.47.03.run --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
    ```

</blockquote></details>

#### 5. Download and install CUDA

```
wget https://developer.download.nvidia.com/compute/cuda/11.6.1/local_installers/cuda_11.6.1_510.47.03_linux.run
sudo sh cuda_11.6.1_510.47.03_linux.run --silent --toolkit
```

* Export environment variables

  ```
  echo $'export PATH=/usr/local/cuda-11.6/bin${PATH:+:${PATH}}\nexport LD_LIBRARY_PATH=/usr/local/cuda-11.6/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}' >> ~/.bashrc && source ~/.bashrc
  ```

#### 6. Download from [NVIDIA website](https://developer.nvidia.com/nvidia-tensorrt-8x-download) and install the TensorRT

TensorRT 8.2 GA Update 4 for Ubuntu 20.04 and CUDA 11.0, 11.1, 11.2, 11.3, 11.4 and 11.5 DEB local repo Package

```
sudo dpkg -i nv-tensorrt-repo-ubuntu2004-cuda11.4-trt8.2.5.1-ga-20220505_1-1_amd64.deb
sudo apt-key add /var/nv-tensorrt-repo-ubuntu2004-cuda11.4-trt8.2.5.1-ga-20220505/82307095.pub
sudo apt-get update
sudo apt-get install libnvinfer8=8.2.5-1+cuda11.4 libnvinfer-plugin8=8.2.5-1+cuda11.4 libnvparsers8=8.2.5-1+cuda11.4 libnvonnxparsers8=8.2.5-1+cuda11.4 libnvinfer-bin=8.2.5-1+cuda11.4 libnvinfer-dev=8.2.5-1+cuda11.4 libnvinfer-plugin-dev=8.2.5-1+cuda11.4 libnvparsers-dev=8.2.5-1+cuda11.4 libnvonnxparsers-dev=8.2.5-1+cuda11.4 libnvinfer-samples=8.2.5-1+cuda11.4 libnvinfer-doc=8.2.5-1+cuda11.4 libcudnn8-dev=8.4.0.27-1+cuda11.6 libcudnn8=8.4.0.27-1+cuda11.6
sudo apt-mark hold libnvinfer* libnvparsers* libnvonnxparsers* libcudnn8* tensorrt
```

#### 7. Download from [NVIDIA website](https://developer.nvidia.com/deepstream-sdk-download-tesla-archived) and install the DeepStream SDK

DeepStream 6.1 for Servers and Workstations (.deb)

```
sudo apt-get install ./deepstream-6.1_6.1.0-1_amd64.deb
rm ${HOME}/.cache/gstreamer-1.0/registry.x86_64.bin
sudo ln -snf /usr/local/cuda-11.6 /usr/local/cuda
```

#### 8. Reboot the computer

```
sudo reboot
```

</details>

<details><summary>DeepStream 6.0.1 / 6.0</summary>

#### 1. Disable Secure Boot in BIOS

<details><summary>If you are using a laptop with newer Intel/AMD processors and your Graphics in Settings->Details->About tab is llvmpipe, please update the kernel.</summary>

```
wget https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.11/amd64/linux-headers-5.11.0-051100_5.11.0-051100.202102142330_all.deb
wget https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.11/amd64/linux-headers-5.11.0-051100-generic_5.11.0-051100.202102142330_amd64.deb
wget https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.11/amd64/linux-image-unsigned-5.11.0-051100-generic_5.11.0-051100.202102142330_amd64.deb
wget https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.11/amd64/linux-modules-5.11.0-051100-generic_5.11.0-051100.202102142330_amd64.deb
sudo dpkg -i  *.deb
sudo reboot
```

</details>

#### 2. Install dependencies

```
sudo apt-get update
sudo apt-get install gcc make git libtool autoconf autogen pkg-config cmake
sudo apt-get install python3 python3-dev python3-pip
sudo apt-get install libssl1.0.0 libgstreamer1.0-0 gstreamer1.0-tools gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly gstreamer1.0-libav libgstrtspserver-1.0-0 libjansson4
sudo apt-get install linux-headers-$(uname -r)
```

**NOTE**: Install DKMS only if you are using the default Ubuntu kernel

```
sudo apt-get install dkms
```

**NOTE**: Purge all NVIDIA driver, CUDA, etc (replace $CUDA_PATH to your CUDA path)

```
sudo nvidia-uninstall
sudo $CUDA_PATH/bin/cuda-uninstaller
sudo apt-get remove --purge '*nvidia*'
sudo apt-get remove --purge '*cuda*'
sudo apt-get remove --purge '*cudnn*'
sudo apt-get remove --purge '*tensorrt*'
sudo apt autoremove --purge && sudo apt autoclean && sudo apt clean
```

#### 3. Install CUDA Keyring

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-keyring_1.0-1_all.deb
sudo dpkg -i cuda-keyring_1.0-1_all.deb
sudo apt-get update
```

#### 4. Download and install NVIDIA Driver

<details><summary>TITAN, GeForce RTX / GTX series and RTX / Quadro series</summary><blockquote>

- Download

  ```
  wget https://us.download.nvidia.com/XFree86/Linux-x86_64/470.129.06/NVIDIA-Linux-x86_64-470.129.06.run
  ```

<blockquote><details><summary>Laptop</summary>

* Run

  ```
  sudo sh NVIDIA-Linux-x86_64-470.129.06.run --silent --disable-nouveau --dkms --install-libglvnd
  ```

  **NOTE**: This step will disable the nouveau drivers.

  **NOTE**: Remove --dkms flag if you installed the 5.11.0 kernel.

* Reboot

  ```
  sudo reboot
  ```

* Install

  ```
  sudo sh NVIDIA-Linux-x86_64-470.129.06.run --silent --disable-nouveau --dkms --install-libglvnd
  ```

  **NOTE**: Remove --dkms flag if you installed the 5.11.0 kernel.

**NOTE**: If you are using a laptop with NVIDIA Optimius, run

```
sudo apt-get install nvidia-prime
sudo prime-select nvidia
```

</details></blockquote>

<blockquote><details><summary>Desktop</summary>

* Run

  ```
  sudo sh NVIDIA-Linux-x86_64-470.129.06.run --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
  ```

  **NOTE**: This step will disable the nouveau drivers.

  **NOTE**: Remove --dkms flag if you installed the 5.11.0 kernel.

* Reboot

  ```
  sudo reboot
  ```

* Install

  ```
  sudo sh NVIDIA-Linux-x86_64-470.129.06.run --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
  ```

  **NOTE**: Remove --dkms flag if you installed the 5.11.0 kernel.

</details></blockquote>

</blockquote></details>

<details><summary>Data center / Tesla series</summary><blockquote>

  - Download

    ```
    wget https://us.download.nvidia.com/tesla/470.129.06/NVIDIA-Linux-x86_64-470.129.06.run
    ```

  * Run

    ```
    sudo sh NVIDIA-Linux-x86_64-470.129.06.run --silent --disable-nouveau --dkms --install-libglvnd --run-nvidia-xconfig
    ```

    **NOTE**: Remove --dkms flag if you installed the 5.11.0 kernel.

</blockquote></details>

#### 5. Download and install CUDA

```
wget https://developer.download.nvidia.com/compute/cuda/11.4.1/local_installers/cuda_11.4.1_470.57.02_linux.run
sudo sh cuda_11.4.1_470.57.02_linux.run --silent --toolkit
```

* Export environment variables

  ```
  echo $'export PATH=/usr/local/cuda-11.4/bin${PATH:+:${PATH}}\nexport LD_LIBRARY_PATH=/usr/local/cuda-11.4/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}' >> ~/.bashrc && source ~/.bashrc
  ```

#### 6. Download from [NVIDIA website](https://developer.nvidia.com/nvidia-tensorrt-8x-download) and install the TensorRT

TensorRT 8.0.1 GA for Ubuntu 18.04 and CUDA 11.3 DEB local repo package

```
sudo dpkg -i nv-tensorrt-repo-ubuntu1804-cuda11.3-trt8.0.1.6-ga-20210626_1-1_amd64.deb
sudo apt-key add /var/nv-tensorrt-repo-ubuntu1804-cuda11.3-trt8.0.1.6-ga-20210626/7fa2af80.pub
sudo apt-get update
sudo apt-get install libnvinfer8=8.0.1-1+cuda11.3 libnvinfer-plugin8=8.0.1-1+cuda11.3 libnvparsers8=8.0.1-1+cuda11.3 libnvonnxparsers8=8.0.1-1+cuda11.3 libnvinfer-bin=8.0.1-1+cuda11.3 libnvinfer-dev=8.0.1-1+cuda11.3 libnvinfer-plugin-dev=8.0.1-1+cuda11.3 libnvparsers-dev=8.0.1-1+cuda11.3 libnvonnxparsers-dev=8.0.1-1+cuda11.3 libnvinfer-samples=8.0.1-1+cuda11.3 libnvinfer-doc=8.0.1-1+cuda11.3 libcudnn8-dev=8.2.1.32-1+cuda11.3 libcudnn8=8.2.1.32-1+cuda11.3
sudo apt-mark hold libnvinfer* libnvparsers* libnvonnxparsers* libcudnn8* tensorrt
```

#### 7. Download from [NVIDIA website](https://developer.nvidia.com/deepstream-sdk-download-tesla-archived) and install the DeepStream SDK

* DeepStream 6.0.1 for Servers and Workstations (.deb)

  ```
  sudo apt-get install ./deepstream-6.0_6.0.1-1_amd64.deb
  ```

* DeepStream 6.0 for Servers and Workstations (.deb)

  ```
  sudo apt-get install ./deepstream-6.0_6.0.0-1_amd64.deb
  ```

* Run

  ```
  rm ${HOME}/.cache/gstreamer-1.0/registry.x86_64.bin
  sudo ln -snf /usr/local/cuda-11.4 /usr/local/cuda
  ```

#### 8. Reboot the computer

```
sudo reboot
```

</details>

##

### Basic usage

#### 1. Download the repo

```
git clone https://github.com/marcoslucianops/DeepStream-Yolo.git
cd DeepStream-Yolo
```

#### 2. Download the `cfg` and `weights` files from [Darknet](https://github.com/AlexeyAB/darknet) repo to the DeepStream-Yolo folder

#### 3. Compile the lib

* DeepStream 6.2 on x86 platform

  ```
  CUDA_VER=11.8 make -C nvdsinfer_custom_impl_Yolo
  ```

* DeepStream 6.1.1 on x86 platform

  ```
  CUDA_VER=11.7 make -C nvdsinfer_custom_impl_Yolo
  ```

* DeepStream 6.1 on x86 platform

  ```
  CUDA_VER=11.6 make -C nvdsinfer_custom_impl_Yolo
  ```

* DeepStream 6.0.1 / 6.0 on x86 platform

  ```
  CUDA_VER=11.4 make -C nvdsinfer_custom_impl_Yolo
  ```

* DeepStream 6.2 / 6.1.1 / 6.1 on Jetson platform

  ```
  CUDA_VER=11.4 make -C nvdsinfer_custom_impl_Yolo
  ```

* DeepStream 6.0.1 / 6.0 on Jetson platform

  ```
  CUDA_VER=10.2 make -C nvdsinfer_custom_impl_Yolo
  ```

#### 4. Edit the `config_infer_primary.txt` file according to your model (example for YOLOv4)

```
[property]
...
custom-network-config=yolov4.cfg
model-file=yolov4.weights
...
```

#### 5. Run

```
deepstream-app -c deepstream_app_config.txt
```

**NOTE**: The TensorRT engine file may take a very long time to generate (sometimes more than 10 minutes).

**NOTE**: If you want to use YOLOv2 or YOLOv2-Tiny models, change the `deepstream_app_config.txt` file before run it

```
...
[primary-gie]
...
config-file=config_infer_primary_yoloV2.txt
...
```

##

### Docker usage

* x86 platform

  ```
  nvcr.io/nvidia/deepstream:6.2-devel
  nvcr.io/nvidia/deepstream:6.2-triton
  ```

* Jetson platform

  ```
  nvcr.io/nvidia/deepstream-l4t:6.2-samples
  nvcr.io/nvidia/deepstream-l4t:6.2-triton
  ```

  **NOTE**: To compile the `nvdsinfer_custom_impl_Yolo`, you need to install the g++ inside the container

  ```
  apt-get install build-essential
  ```

  **NOTE**: With DeepStream 6.2, the docker containers do not package libraries necessary for certain multimedia operations like audio data parsing, CPU decode, and CPU encode. This change could affect processing certain video streams/files like mp4 that include audio track. Please run the below script inside the docker images to install additional packages that might be necessary to use all of the DeepStreamSDK features:
  
  ```
  /opt/nvidia/deepstream/deepstream/user_additional_install.sh
  ```

##

### NMS Configuration

To change the `nms-iou-threshold`, `pre-cluster-threshold` and `topk` values, modify the config_infer file

```
[class-attrs-all]
nms-iou-threshold=0.45
pre-cluster-threshold=0.25
topk=300
```

**NOTE**: Make sure to set `cluster-mode=2` in the config_infer file.

##

### INT8 calibration

**NOTE**: For now, Only for Darknet YOLO model.

#### 1. Install OpenCV

```
sudo apt-get install libopencv-dev
```

#### 2. Compile/recompile the `nvdsinfer_custom_impl_Yolo` lib with OpenCV support

* DeepStream 6.2 on x86 platform

  ```
  CUDA_VER=11.8 OPENCV=1 make -C nvdsinfer_custom_impl_Yolo
  ```

* DeepStream 6.1.1 on x86 platform

  ```
  CUDA_VER=11.7 OPENCV=1 make -C nvdsinfer_custom_impl_Yolo
  ```

* DeepStream 6.1 on x86 platform

  ```
  CUDA_VER=11.6 OPENCV=1 make -C nvdsinfer_custom_impl_Yolo
  ```

* DeepStream 6.0.1 / 6.0 on x86 platform

  ```
  CUDA_VER=11.4 OPENCV=1 make -C nvdsinfer_custom_impl_Yolo
  ```

* DeepStream 6.2 / 6.1.1 / 6.1 on Jetson platform

  ```
  CUDA_VER=11.4 OPENCV=1 make -C nvdsinfer_custom_impl_Yolo
  ```

* DeepStream 6.0.1 / 6.0 on Jetson platform

  ```
  CUDA_VER=10.2 OPENCV=1 make -C nvdsinfer_custom_impl_Yolo
  ```

#### 3. For COCO dataset, download the [val2017](https://drive.google.com/file/d/1gbvfn7mcsGDRZ_luJwtITL-ru2kK99aK/view?usp=sharing), extract, and move to DeepStream-Yolo folder

* Select 1000 random images from COCO dataset to run calibration

  ```
  mkdir calibration
  ```

  ```
  for jpg in $(ls -1 val2017/*.jpg | sort -R | head -1000); do \
      cp ${jpg} calibration/; \
  done
  ```

* Create the `calibration.txt` file with all selected images

  ```
  realpath calibration/*jpg > calibration.txt
  ```

* Set environment variables

  ```
  export INT8_CALIB_IMG_PATH=calibration.txt
  export INT8_CALIB_BATCH_SIZE=1
  ```

* Edit the `config_infer` file

  ```
  ...
  model-engine-file=model_b1_gpu0_fp32.engine
  #int8-calib-file=calib.table
  ...
  network-mode=0
  ...
  ```

    To

  ```
  ...
  model-engine-file=model_b1_gpu0_int8.engine
  int8-calib-file=calib.table
  ...
  network-mode=1
  ...
  ```

* Run

  ```
  deepstream-app -c deepstream_app_config.txt
  ```

**NOTE**: NVIDIA recommends at least 500 images to get a good accuracy. On this example, I recommend to use 1000 images to get better accuracy (more images = more accuracy). Higher `INT8_CALIB_BATCH_SIZE` values will result in more accuracy and faster calibration speed. Set it according to you GPU memory. This process may take a long time.

##

### Extract metadata

You can get metadata from DeepStream using Python and C/C++. For C/C++, you can edit the `deepstream-app` or `deepstream-test` codes. For Python, your can install and edit [deepstream_python_apps](https://github.com/NVIDIA-AI-IOT/deepstream_python_apps).

Basically, you need manipulate the `NvDsObjectMeta` ([Python](https://docs.nvidia.com/metropolis/deepstream/python-api/PYTHON_API/NvDsMeta/NvDsObjectMeta.html) / [C/C++](https://docs.nvidia.com/metropolis/deepstream/sdk-api/struct__NvDsObjectMeta.html)) `and NvDsFrameMeta` ([Python](https://docs.nvidia.com/metropolis/deepstream/python-api/PYTHON_API/NvDsMeta/NvDsFrameMeta.html) / [C/C++](https://docs.nvidia.com/metropolis/deepstream/sdk-api/struct__NvDsFrameMeta.html)) to get the label, position, etc. of bboxes.

##

My projects: https://www.youtube.com/MarcosLucianoTV
