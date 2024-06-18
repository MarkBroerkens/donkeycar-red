# donkeycar-red
[Donkeycar](http://www.donkeycar.com) with Jetson nano.

* [nvidia JetPack 4.6.4](https://developer.nvidia.com/jetpack-sdk-464)
* [donkeycar 4.5.1](https://github.com/autorope/donkeycar/tree/4.5.1)
* [Tensorflow 2.7](https://github.com/tensorflow/tensorflow/releases/tag/v2.7.0)

## Hardware Setup



## Software Setup
https://docs.donkeycar.com/guide/robot_sbc/setup_jetson_nano/

* host name: donkeycar-red
* user: donkey
* password: DonkeyCar
* locale settings: Berlin
* keyboard layout: en

### Step 1a: Flash Operating System
get the latest JetPack that supports the Jetson nano.
[nvidia JetPack 4.6.4](https://developer.nvidia.com/jetpack-sdk-464)

follow [getting started tutorial](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#write)

Remove Libre Office:

```shell
sudo apt-get remove --purge libreoffice*
sudo apt-get clean
sudo apt-get autoremove
```

And add a 8GB swap file:


```shell
git clone https://github.com/JetsonHacksNano/installSwapfile
cd installSwapfile
./installSwapfile.sh
sudo reboot now 
```

### Step 3a: Install System-Wide Dependencies
First install some packages with apt-get.

```shell
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install -y libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran
sudo apt-get install -y python3-dev python3-pip
sudo apt-get install -y libxslt1-dev libxml2-dev libffi-dev libcurl4-openssl-dev libssl-dev libpng-dev libopenblas-dev
sudo apt-get install -y git nano
sudo apt-get install -y openmpi-doc openmpi-bin libopenmpi-dev libopenblas-dev
```

### Step 4a: Setup Python Environment.
#### Setup Virtual Environment

```shell
pip3 install virtualenv
python3 -m virtualenv -p python3 env --system-site-packages
echo "source ~/env/bin/activate" >> ~/.bashrc
source ~/.bashrc
```


#### Setup Python Dependencies
Next, you will need to install packages with pip:

```shell
pip3 install -U pip testresources setuptools
pip3 install -U futures==3.1.1 protobuf==3.12.2 pybind11==2.5.0
pip3 install -U cython==0.29.21 pyserial
pip3 install -U future==0.18.2 mock==4.0.2 h5py==3.1.0 keras_preprocessing==1.1.2 keras_applications==1.0.8 gast==0.3.3
pip3 install -U absl-py==0.9.0 py-cpuinfo==7.0.0 psutil==5.7.2 portpicker==1.3.1 six requests==2.24.0 astor==0.8.1 termcolor==1.1.0 wrapt==1.12.1 google-pasta==0.2.0
pip3 install -U gdown
```


and tensorflow:

* https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform-release-notes/tf-jetson-rel.html#tf-jetson-rel
* https://jetson-docs.com/libraries/tensorflow/l4t32.7.1/py3.6.9
* https://developer.download.nvidia.com/compute/redist/jp/v461/tensorflow/

```shell
sudo apt-get update
sudo apt-get install -y python3-pip pkg-config
sudo apt-get install -y libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran
sudo ln -s /usr/include/locale.h /usr/include/xlocale.h
wget --no-check-certificate https://developer.download.nvidia.com/compute/redist/jp/v461/tensorflow/tensorflow-2.7.0+nv22.1-cp36-cp36m-linux_aarch64.whl
pip3 install --verbose tensorflow-2.7.0+nv22.1-cp36-cp36m-linux_aarch64.whl

pip3 install keras==2.6

```

#### Install Donkeycar Python Code
```shell
mkdir projects
cd ~/projects
git clone https://github.com/autorope/donkeycar
cd donkeycar
git fetch --all --tags -f
git checkout 4.5.1
pip install -e .[nano]
```

# configure camera
```shell
To resolve this issue, enter the following commands:
$ sudo mkdir /boot/dtb
$ sudo cp -v /boot/tegra210-p3448-0000-p3449-0000-[ab]0[02].dtb /boot/dtb/
```

```
sudo /opt/nvidia/jetson-io/jetson-io.py
```



