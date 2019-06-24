# Configuration-DL
Instructions for DL configuration


Software
Linux Ubuntu 16.04.6 LTS (GNU/Linux 4.15.0-47-generic x86_64)
Driver 410.79


Hardware
2 Quadro k5000 compute capability 3.0

# Remove previous NVIDIA software installations and install driver 430

Github page to install drivers from source and via apt-get
https://gist.github.com/wangruohui/df039f0dc434d6486f5d4d098aa52d07

430 driver was built with gcc-5.4 but seems to work well with gcc-5.5


# Install CUDA
Download from https://developer.nvidia.com/cuda-90-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1604&target_type=runfilelocal
runfile local installer type

Follow the instructions on the web page
reboot the system and validate installation with nvcc --version
install patches 

# Install cudnn 7.5
Download from the NVIDIA web page
https://developer.nvidia.com/compute/machine-learning/cudnn/secure/v7.5.0.56/prod/9.0_20190219/cudnn-9.0-linux-x64-v7.5.0.56.tgz

Follow installation instructions from:
https://docs.nvidia.com/deeplearning/sdk/cudnn-install/index.html

Verify your cudnn installation
cat /usr/local/cuda/include/cudnn.h | grep CUDNN_MAJOR -A 2
or
cat /usr/include/cudnn.h | grep CUDNN_MAJOR -A 2

# Tensorflow and Keras
Consider to create a virtual environment with python3 
https://docs.python-guide.org/dev/virtualenvs/

Install alt model checkpoint which allow to save best model using multiple gpus [only available for python3]
pip install alt-model-checkpoint

Reference [https://www.textpert.ai/aime-blog/saving-multi-gpu-models-with-keras-modelcheckpoint]



### Tensorflow [version '1.8.0']
Build tensorflow from source to allow multiple gpu usage due to gpus compute capability 3.0

Check the table with neccesary requirements

Is necessary to work with the appropiate gcc compiler 

Page to switch between gcc compilers
https://askubuntu.com/questions/313288/how-to-use-multiple-instances-of-gcc

Here are two tutorials to build tensorflow from source. If you previously create a virtual environment to work in, consider to activate before build tensorflow

https://medium.com/@saitejadommeti/building-tensorflow-gpu-from-source-for-rtx-2080-96fed102fcca
https://medium.com/@Oysiyl/install-tensorflow-1-8-0-with-gpu-from-source-on-ubuntu-18-04-bionic-beaver-35cfa9df3600

Consider to replace 
git checkout r1.11
with
git checkout r1.8
this will depend on the tensorflow version you are looking for. In my case varsion 1.8.0 was installed


### Keras [version 2.2.4]
pip install keras
### Pytorch [version 0.3.0]
pip install --user http://download.pytorch.org/whl/cu80/torch-0.3.0-cp27-cp27mu-linux_x86_64.whl
