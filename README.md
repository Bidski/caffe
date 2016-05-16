# OpenCL Caffe

**This is an experimental, community-maintained branch led by Fabian Tschopp (@naibaf7). It is a work-in-progress.**

**For error reports, please run and include the result of `./build/test/test_all.testbin --gtest_filter=*OpenCLKernelCompileTest* X` where `X` is the OpenCL device to test (i.e. `0`). This test is available after a build with `make all`, `make runtest`.**

This branch of Caffe contains an OpenCL backend and additional layers for fast image segmentation.
This work is partially supported by:
- AMD
- HHMI Janelia
- UZH, INI
- ETH Zurich
- Intel

For a C++ frontend and models to use for image segmentation with this fork, see:
- Frontend: https://github.com/naibaf7/caffe_neural_tool
- Models: https://github.com/naibaf7/caffe_neural_models

## OpenCL Backend

The backend is supposed to work with all vendors. Note however there may be problems with libOpenCL.so provided by nVidia.
It is therefore recommended to install another OpenCL implementation after installing nVidia drivers. Possibilities are:
- Intel OpenCL, see https://github.com/01org/caffe/wiki/clCaffe for details. 
- AMD APP SDK (OpenCL), recommended if you have an AMD GPU or CPU.

## Technical Report
Available on arXiv:
http://arxiv.org/abs/1509.03371


# Windows Caffe

**This is an experimental, communtity based branch led by Guillaume Dumont (@willyd). It is a work-in-progress.**

This branch of Caffe ports the framework to Windows.

[![Travis Build Status](https://api.travis-ci.org/BVLC/caffe.svg?branch=windows)](https://travis-ci.org/BVLC/caffe) Travis (Linux build)

[![Build status](https://ci.appveyor.com/api/projects/status/ew7cl2k1qfsnyql4/branch/windows?svg=true)](https://ci.appveyor.com/project/BVLC/caffe/branch/windows) AppVeyor (Windows build)

## Prebuilt binaries

Prebuilt binaries can be downloaded from the latest CI build on appveyor for the following configurations:

- Visual Studio 2015, CPU only, Python 3.5: [Caffe Release](https://ci.appveyor.com/api/projects/BVLC/caffe/artifacts/build/caffe.zip?branch=windows&job=Environment%3A%20MSVC_VERSION%3D14%2C%20WITH_NINJA%3D0%2C%20CMAKE_CONFIG%3DRelease%2C%20CMAKE_BUILD_SHARED_LIBS%3D0%2C%20PYTHON_VERSION%3D3%2C%20WITH_CUDA%3D0), ~~[Caffe Debug](https://ci.appveyor.com/api/projects/BVLC/caffe/artifacts/build/caffe.zip?branch=windows&job=Environment%3A%20MSVC_VERSION%3D14%2C%20WITH_NINJA%3D0%2C%20CMAKE_CONFIG%3DDebug%2C%20CMAKE_BUILD_SHARED_LIBS%3D0%2C%20PYTHON_VERSION%3D3%2C%20WITH_CUDA%3D0)~~

- Visual Studio 2015, CUDA 8.0, Python 3.5: [Caffe Release](https://ci.appveyor.com/api/projects/BVLC/caffe/artifacts/build/caffe.zip?branch=windows&job=Environment%3A%20MSVC_VERSION%3D14%2C%20WITH_NINJA%3D1%2C%20CMAKE_CONFIG%3DRelease%2C%20CMAKE_BUILD_SHARED_LIBS%3D0%2C%20PYTHON_VERSION%3D3%2C%20WITH_CUDA%3D1)

- Visual Studio 2015, CPU only, Python 2.7: [Caffe Release](https://ci.appveyor.com/api/projects/BVLC/caffe/artifacts/build/caffe.zip?branch=windows&job=Environment%3A%20MSVC_VERSION%3D14%2C%20WITH_NINJA%3D0%2C%20CMAKE_CONFIG%3DRelease%2C%20CMAKE_BUILD_SHARED_LIBS%3D0%2C%20PYTHON_VERSION%3D2%2C%20WITH_CUDA%3D0), [Caffe Debug](https://ci.appveyor.com/api/projects/BVLC/caffe/artifacts/build/caffe.zip?branch=windows&job=Environment%3A%20MSVC_VERSION%3D14%2C%20WITH_NINJA%3D0%2C%20CMAKE_CONFIG%3DDebug%2C%20CMAKE_BUILD_SHARED_LIBS%3D0%2C%20PYTHON_VERSION%3D2%2C%20WITH_CUDA%3D0)

- Visual Studio 2015,CUDA 8.0, Python 2.7: [Caffe Release](https://ci.appveyor.com/api/projects/BVLC/caffe/artifacts/build/caffe.zip?branch=windows&job=Environment%3A%20MSVC_VERSION%3D14%2C%20WITH_NINJA%3D1%2C%20CMAKE_CONFIG%3DRelease%2C%20CMAKE_BUILD_SHARED_LIBS%3D0%2C%20PYTHON_VERSION%3D2%2C%20WITH_CUDA%3D1)

- Visual Studio 2013, CPU only, Python 2.7: [Caffe Release](https://ci.appveyor.com/api/projects/BVLC/caffe/artifacts/build/caffe.zip?branch=windows&job=Environment%3A%20MSVC_VERSION%3D12%2C%20WITH_NINJA%3D0%2C%20CMAKE_CONFIG%3DRelease%2C%20CMAKE_BUILD_SHARED_LIBS%3D0%2C%20PYTHON_VERSION%3D2%2C%20WITH_CUDA%3D0), [Caffe Debug](https://ci.appveyor.com/api/projects/BVLC/caffe/artifacts/build/caffe.zip?branch=windows&job=Environment%3A%20MSVC_VERSION%3D12%2C%20WITH_NINJA%3D0%2C%20CMAKE_CONFIG%3DDebug%2C%20CMAKE_BUILD_SHARED_LIBS%3D0%2C%20PYTHON_VERSION%3D2%2C%20WITH_CUDA%3D0)


## Windows Setup

### Requirements

 - Visual Studio 2013 or 2015
 - [CMake](https://cmake.org/) 3.4 or higher (Visual Studio and [Ninja](https://ninja-build.org/) generators are supported)

### Optional Dependencies

 - Python for the pycaffe interface. Anaconda Python 2.7 or 3.5 x64 (or Miniconda)
 - Matlab for the matcaffe interface.
 - CUDA 7.5 or 8.0 (use CUDA 8 if using Visual Studio 2015)
 - cuDNN v5

 We assume that `cmake.exe` and `python.exe` are on your `PATH`.

### Configuring and Building Caffe

The fastest method to get started with caffe on Windows is by executing the following commands in a `cmd` prompt (we use `C:\Projects` as a root folder for the remainder of the instructions):
```cmd
C:\Projects> git clone https://github.com/BVLC/caffe.git
C:\Projects> cd caffe
C:\Projects\caffe> git checkout windows
:: Edit any of the options inside build_win.cmd to suit your needs
C:\Projects\caffe> scripts\build_win.cmd
```
The `build_win.cmd` script will download the dependencies, create the Visual Studio project files (or the ninja build files) and build the Release configuration. By default all the required DLLs will be copied (or hard linked when possible) next to the consuming binaries. If you wish to disable this option, you can by changing the command line option `-DCOPY_PREREQUISITES=0`. The prebuilt libraries also provide a `prependpath.bat` batch script that can temporarily modify your `PATH` envrionment variable to make the required DLLs available.

Below is a more complete description of some of the steps involved in building caffe.

### Install the caffe dependencies

By default CMake will download and extract prebuilt dependencies for your compiler and python version. It will create a folder called `libraries` containing all the required dependencies inside your build folder. Alternatively you can build them yourself by following the instructions in the [caffe-builder](https://github.com/willyd/caffe-builder) [README](https://github.com/willyd/caffe-builder/blob/master/README.md).

### Use cuDNN

To use cuDNN the easiest way is to copy the content of the `cuda` folder into your CUDA toolkit installation directory. For example if you installed CUDA 8.0 and downloaded cudnn-8.0-windows10-x64-v5.1.zip you should copy the content of the `cuda` directory to `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0`. Alternatively, you can define the CUDNN_ROOT cache variable to point to where you unpacked the cuDNN files e.g. `C:/Projects/caffe/cudnn-8.0-windows10-x64-v5.1/cuda`. For example the command in [scripts/build_win.cmd](scripts/build_win.cmd) would become:
```
cmake -G"!CMAKE_GENERATOR!" ^
      -DBLAS=Open ^
      -DCMAKE_BUILD_TYPE:STRING=%CMAKE_CONFIG% ^
      -DBUILD_SHARED_LIBS:BOOL=%CMAKE_BUILD_SHARED_LIBS% ^
      -DBUILD_python:BOOL=%BUILD_PYTHON% ^
      -DBUILD_python_layer:BOOL=%BUILD_PYTHON_LAYER% ^
      -DBUILD_matlab:BOOL=%BUILD_MATLAB% ^
      -DCPU_ONLY:BOOL=%CPU_ONLY% ^
      -DCUDNN_ROOT=C:/Projects/caffe/cudnn-8.0-windows10-x64-v5.1/cuda ^
      -C "%cd%\libraries\caffe-builder-config.cmake" ^
      "%~dp0\.."
```

Alternatively, you can open `cmake-gui.exe` and set the variable from there and click `Generate`.

### Building only for CPU

If CUDA is not installed Caffe will default to a CPU_ONLY build. If you have CUDA installed but want a CPU only build you may use the CMake option `-DCPU_ONLY=1`.

### Using the Python interface

The recommended Python distribution is Anaconda or Miniconda. To successfully build the python interface you need to install the following packages:
```
conda install --yes numpy scipy matplotlib scikit-image pip six
```
also you will need a protobuf python package that is compatible with pre-built dependencies. This package can be installed this way:
```
conda install --yes --channel willyd protobuf==3.1.0
```
If Python is installed the default is to build the python interface and python layers. If you wish to disable the python layers or the python build use the CMake options `-DBUILD_python_layer=0` and `-DBUILD_python=0` respectively. In order to use the python interface you need to either add the `C:\Projects\caffe\python` folder to your python path of copy the `C:\Projects\caffe\python\caffe` folder to your `site_packages` folder.

### Using the MATLAB interface

Follow the above procedure and use `-DBUILD_matlab=ON`. Change your current directory in MATLAB to `C:\Projects\caffe\matlab` and run the following command to run the tests:
```
>> caffe.run_tests()
```
If all tests pass you can test if the classification_demo works as well. First, from `C:\Projects\caffe` run `python scripts\download_model_binary.py models\bvlc_reference_caffenet` to download the pre-trained caffemodel from the model zoo. Then change your MATLAB directory to `C:\Projects\caffe\matlab\demo` and run `classification_demo`.

### Using the Ninja generator

You can choose to use the Ninja generator instead of Visual Studio for faster builds. To do so, change the option `set WITH_NINJA=1` in the `build_win.cmd` script. To install Ninja you can download the executable from github or install it via conda:
```cmd
> conda config --add channels conda-forge
> conda install ninja --yes
```
When working with ninja you don't have the Visual Studio solutions as ninja is more akin to make. An alternative is to use [Visual Studio Code](https://code.visualstudio.com) with the CMake extensions and C++ extensions.

### Building a shared library

CMake can be used to build a shared library instead of the default static library. To do so follow the above procedure and use `-DBUILD_SHARED_LIBS=ON`. Please note however, that some tests (more specifically the solver related tests) will fail since both the test exectuable and caffe library do not share static objects contained in the protobuf library.

### Troubleshooting

Should you encounter any error please post the output of the above commands by redirecting the output to a file and open a topic on the [caffe-users list](https://groups.google.com/forum/#!forum/caffe-users) mailing list.

## Previous Visual Studio based build

The previous windows build based on Visual Studio project files is now deprecated. However, it is still available in the `windows` folder. Please see the [README.md](windows/README.md) in there for details.

## Known issues

- The `GPUTimer` related test cases always fail on Windows. This seems to be a difference between UNIX and Windows.
- Shared library (DLL) build will have failing tests.
- Shared library build only works with the Ninja generator

## Further Details

Refer to the BVLC/caffe master branch README for all other details such as license, citation, and so on.

# SSD: Single Shot MultiBox Detector

By [Wei Liu](http://www.cs.unc.edu/~wliu/), [Dragomir Anguelov](http://research.google.com/pubs/DragomirAnguelov.html), [Dumitru Erhan](http://research.google.com/pubs/DumitruErhan.html), [Christian Szegedy](http://research.google.com/pubs/ChristianSzegedy.html), [Scott Reed](http://www-personal.umich.edu/~reedscot/), Cheng-Yang Fu, [Alexander C. Berg](http://acberg.com).

### Introduction

SSD is an unified framework for object detection with a single network. You can use the code to train/evaluate a network for object detection task. For more details, please refer to our [arXiv paper](http://arxiv.org/abs/1512.02325).

<p align="center">
<img src="http://www.cs.unc.edu/~wliu/papers/ssd.png" alt="SSD Framework" width="600px">
</p>

<center>

| System | VOC2007 test *mAP* | **FPS** (Titan X) | Number of Boxes |
|:-------|:-----:|:-------:|:-------:|
| [Faster R-CNN (VGG16)](https://github.com/ShaoqingRen/faster_rcnn) | 73.2 | 7 | 300 |
| [Faster R-CNN (ZF)](https://github.com/ShaoqingRen/faster_rcnn) | 62.1 | 17 | 300 |
| [YOLO](http://pjreddie.com/darknet/yolo/) | 63.4 | 45 | 98 |
| [Fast YOLO](http://pjreddie.com/darknet/yolo/) | 52.7 | 155 | 98 |
| SSD300 (VGG16) | 72.1 | 58 | 7308 |
| SSD500 (VGG16) | **75.1** | 23 | 20097 |

</center>

### Citing SSD

Please cite SSD in your publications if it helps your research:

    @article{liu15ssd,
      Title = {{SSD}: Single Shot MultiBox Detector},
      Author = {Liu, Wei and Anguelov, Dragomir and Erhan, Dumitru and Szegedy, Christian and Reed, Scott},
      Journal = {arXiv preprint arXiv:1512.02325},
      Year = {2015}
    }

### Contents
1. [Installation](#installation)
2. [Preparation](#preparation)
3. [Train/Eval](#traineval)
4. [Models](#models)
4. [Contact](#contact)

### Installation
1. Get the code. We will call the directory that you cloned Caffe into `$CAFFE_ROOT`
  ```Shell
  git clone https://github.com/weiliu89/caffe.git
  cd caffe
  git checkout ssd
  ```

2. Build the code. Please follow [Caffe instruction](http://caffe.berkeleyvision.org/installation.html) to install all necessary packages and build it.
  ```Shell
  # Modify Makefile.config according to your Caffe installation.
  cp Makefile.config.example Makefile.config
  make -j8
  # Make sure to include $CAFFE_ROOT/python to your PYTHONPATH.
  make py
  make test -j8
  make runtest
  # If you have multiple GPUs installed in your machine, make runtest might fail. If so, try following:
  export CUDA_VISIBLE_DEVICES=0; make runtest
  ```

### Preparation
1. Download [fully convolutional reduced (atrous) VGGNet](https://gist.github.com/weiliu89/2ed6e13bfd5b57cf81d6). By default, we assume the model is stored in `$CAFFE_ROOT/models/VGGNet/`

2. Download VOC2007 and VOC2012 dataset. By default, we assume the data is stored in `$HOME/data/`
  ```Shell
  # Download the data.
  cd $HOME/data
  wget http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar
  wget http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtrainval_06-Nov-2007.tar
  wget http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtest_06-Nov-2007.tar
  # Extract the data.
  tar -xvf VOCtrainval_11-May-2012.tar
  tar -xvf VOCtrainval_06-Nov-2007.tar
  tar -xvf VOCtest_06-Nov-2007.tar
  ```

3. Create the LMDB file.
  ```Shell
  cd $CAFFE_ROOT
  # Create the trainval.txt, test.txt, and test_name_size.txt in data/VOC0712/
  ./data/VOC0712/create_list.sh
  # You can modify the parameters in create_data.sh if needed.
  # It will create lmdb files for trainval and test with encoded original image:
  #   - $HOME/data/VOCdevkit/VOC0712/lmdb/VOC0712_trainval_lmdb
  #   - $HOME/data/VOCdevkit/VOC0712/lmdb/VOC0712_test_lmdb
  # and make soft links at examples/VOC0712/
  ./data/VOC0712/create_data.sh
  ```

### Train/Eval
1. Train your model and evaluate the model on the fly.
  ```Shell
  # It will create model definition files and save snapshot models in:
  #   - $CAFFE_ROOT/models/VGGNet/VOC0712/SSD_300x300/
  # and job file, log file, and the python script in:
  #   - $CAFFE_ROOT/jobs/VGGNet/VOC0712/SSD_300x300/
  # and save temporary evaluation results in:
  #   - $HOME/data/VOCdevkit/results/VOC2007/SSD_300x300/
  # It should reach 72.* mAP at 60k iterations.
  python examples/ssd/ssd_pascal.py
  ```
  If you don't have time to train your model, you can download a pre-trained model at [here](http://www.cs.unc.edu/~wliu/projects/SSD/models_VGGNet_VOC0712_SSD_300x300.tar.gz).

2. Evaluate the most recent snapshot.
  ```Shell
  # If you would like to test a model you trained, you can do:
  python examples/ssd/score_ssd_pascal.py
  ```

3. Test your model using a webcam. Note: press <kbd>esc</kbd> to stop.
  ```Shell
  # If you would like to attach a webcam to a model you trained, you can do:
  python examples/ssd/ssd_pascal_webcam.py
  ```
  [Here](https://drive.google.com/file/d/0BzKzrI_SkD1_R09NcjM1eElLcWc/view) is a demo video of running a SSD500 model trained on [MSCOCO](http://mscoco.org) dataset.

4. Check out `examples/ssd_detect.ipynb` on how to detect objects using a SSD model.

5. To train on other dataset, please refer to data/OTHERDATASET for more details.
We currently add support for MSCOCO.

### Models
1. Models trained on VOC0712: [SSD300](http://www.cs.unc.edu/~wliu/projects/SSD/models_VGGNet_VOC0712_SSD_300x300.tar.gz), [SSD500](http://www.cs.unc.edu/~wliu/projects/SSD/models_VGGNet_VOC0712_SSD_500x500.tar.gz)

2. Models trained on MSCOCO trainval35k: [SSD300](http://www.cs.unc.edu/~wliu/projects/SSD/models_VGGNet_coco_SSD_300x300.tar.gz), [SSD500](http://www.cs.unc.edu/~wliu/projects/SSD/models_VGGNet_coco_SSD_500x500.tar.gz)

3. Models trained on ILSVRC2015 trainval1: [SSD300](http://www.cs.unc.edu/~wliu/projects/SSD/models_VGGNet_ilsvrc15_SSD_300x300.tar.gz), [SSD500](http://www.cs.unc.edu/~wliu/projects/SSD/models_VGGNet_ilsvrc15_SSD_500x500.tar.gz) (46.4 mAP on val2)

### Contact
Please direct all comments and report all bugs to:

    Wei Liu
    wliu@cs.unc.edu
