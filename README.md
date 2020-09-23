# openvino_manual

Install OpenVINO™ toolkit for Raspbian* OS

Device : Neural Compute Stick 2

Date : 2020-09-22

official reference site : 
https://docs.openvinotoolkit.org/latest/openvino_docs_install_guides_installing_openvino_raspbian.html

Environments:
RaspberryPi 4 4GB RAM
Distributor ID:	Raspbian
Description:	Raspbian GNU/Linux 10 (buster)
Release:	10
Codename:	buster


Requirements:
opencv
Python 3.7.3
cmake 3.13.4


# Source Download
repo : https://download.01.org/opencv/2020/openvinotoolkit/
l_openvino_toolkit_runtime_raspbian_p_2020.4.287.tgz

#Exctract
tar -xf l_openvino_toolkit_runtime_raspbian_p_2020.4.287.tgz

#Rename
mv l_openvino_toolkit_runtime_raspbian_p_2020.4.287 openvino

#Requirement soft install
Reference Site : https://www.pyimagesearch.com/2019/04/08/openvino-opencv-and-movidius-ncs-on-the-raspberry-pi/

sudo apt-get update && sudo apt-get upgrade
sudo apt-get install build-essential cmake unzip pkg-config
sudo apt-get install libjpeg-dev libpng-dev libtiff-dev
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get install libxvidcore-dev libx264-dev
sudo apt-get install libgtk-3-dev
sudo apt-get install libcanberra-gtk*
sudo apt-get install libatlas-base-dev gfortran
sudo apt-get install python3-dev

# Set the environment variables                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         
source ~/Downloads/openvino/bin/setupvars.sh
## or add bottom line at ~/.bashrc 
[setupvars.sh] OpenVINO environment initialized


#Add USB Rules
sudo usermod -a -G users "$(whoami)"
sh ~/Downloads/openvino/install_dependencies/install_NCS_udev_rules.sh


#Build project
mkdir build && cd build
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_CXX_FLAGS="-march=armv7-a" ~/Downloads/openvino/deployment_tools/inference_engine/samples
make -j2 object_detection_sample_ssd
wget --no-check-certificate https://download.01.org/opencv/2020/openvinotoolkit/2020.1/open_model_zoo/models_bin/1/face-detection-adas-0001/FP16/face-detection-adas-0001.bin
wget --no-check-certificate https://download.01.org/opencv/2020/openvinotoolkit/2020.1/open_model_zoo/models_bin/1/face-detection-adas-0001/FP16/face-detection-adas-0001.xml
./armv7l/Release/object_detection_sample_ssd -m face-detection-adas-0001.xml -d MYRIAD -i <path_to_image>





