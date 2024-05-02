# ALARM: automatic liver attenuation estimation
###  [[project page]](https://github.com/MASILab/ALARM/) [[Medical Physcis paper]](https://arxiv.org/ftp/arxiv/papers/1906/1906.09549.pdf) 

The liver attenuation estimations can be achieved from a single CT abdomen scan
<img src="https://github.com/MASILab/ALARM/blob/master/screenshot/alarm.png" width="600px"/>

It has been implemented as a single Docker.
```diff
+ The code and docker are free for noncommercial purposes.
+ The licence.md shows the terms for commercial and for-profit purposes.
- Please cite the following MICCAI/NeuroImage paper, if you used the ALARM liver attenuation estimation.
```
The papers can be found [[Medical Physcis paper]](https://arxiv.org/ftp/arxiv/papers/1906/1906.09549.pdf), whole full citation are

Yuankai Huo, James G. Terry, Jiachen Wang, Sangeeta Nair, Thomas A. Lasko, Barry I. Freedman, Jeffery J. Carr, and Bennett A. Landman. "Fully Automatic Liver Attenuation Estimation combing CNN Segmentation and Morphological Operations." Medical physics (2019).

## Quick Start
#### Get our docker image
```
sudo docker pull hrlblab333/public:liver_attenuation_v3_0_6
```
#### Run ALARM liver attenuation segmentation
You can run the following command or change the "input_dir", then you will have the final segmentation results in output_dir
```
# you need to specify the input directory
export input_dir=/home/input_dir   
# make that directory
sudo mkdir $input_dir
# put dicom images to the $input_dir directly without subfolders
# set output directory
export output_dir=$input_dir/output
#run the docker if your input_dir contains dicom files
sudo nvidia-docker run -it --rm -v $input_dir:/INPUTS/ -v $output_dir:/OUTPUTS hrlblab333/public:liver_attenuation_v3_0_6 /extra/run_deep_wholebody_dicom.sh

#run the docker if your input_dir contains nifti
sudo nvidia-docker run -it --rm -v $input_dir:/INPUTS/ -v $output_dir:/OUTPUTS hrlblab333/public:liver_attenuation_v3_0_6 /extra/run_deep_wholebody_nifti.sh
```
#### Here is a testing scan
https://vanderbilt.box.com/shared/static/zqbsc1fzi5csgo00urstv8666ligkqhk.gz

## Detailed envrioment setting  

#### Testing platform
- Ubuntu 22.04
- cuda 12.4
- Docker version 26.1.1
- NVIDIA Container Runtime version 1.15.0


#### install Docker
```
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt-get update
sudo apt-get install docker-ce
```

#### install Nvidia-Docker
```
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt-get update
sudo apt-get install -y nvidia-docker2
```



## Docker Setup on Windows

This section provides instructions for installing and setting up Docker on a Windows system.

### Installation

**Download Docker Desktop**: Visit the [Docker Desktop](https://docs.docker.com/desktop/install/windows-install/) website and download the installer.
**Run the Installer**: Double-click the downloaded `.exe` file to start the installation.
**Follow the Prompts**: Follow the installation prompts, ensuring to enable WSL2/Hyper-V integration during setup.
**Restart Your Computer**: Restart your computer after installation completes.

### Configuration

**Docker Desktop Settings**: Open Docker Desktop and go to the **Settings** tab.
**Resources**: Navigate to the **Resources** tab and adjust memory allocation, CPUs, and disk space as needed.
**Shared Drives**: Under the **File Sharing** tab, select which drives or directories you want Docker to access.

### Commands and Usage

You can run the following command or change the "input_dir", then you will have the final segmentation results in output_dir
```
# you need to specify the input directory  
set input_dir=C:\data\inputs
# make that directory
mkdir "%input_dir%"
# put dicom images to the $input_dir directly without subfolders
# set output directory
set output_dir=%input_dir%\output
mkdir "%output_dir%"
#run the docker if your input_dir contains dicom files
docker run -it --rm -v %input_dir%:/INPUTS -v %output_dir%:/OUTPUTS hrlblab333/public:liver_attenuation_v3_0_6 /extra/run_deep_wholebody_dicom.sh

#run the docker if your input_dir contains nifti
docker run -it --rm -v %input_dir%:/INPUTS -v %output_dir%:/OUTPUTS hrlblab333/public:liver_attenuation_v3_0_6 /extra/run_deep_wholebody_nifti.sh

```


[Version Updates]
2023-05-1: update the v3.0.6 from v3.0.4. Update python version from py27 to py38
2022-04-13: update the v3.0.4 from v3.0.3. Address the problem with JP-LS compressed dicom images. Update dcm2niix version to v1.0.20211006 (JP2:OpenJPEG) (JP-LS:CharLS)
2020-02-08: update the v3.0.3 from v3.0.2. Add a pdf generation function to generate a pdf report
2019-08-03: update the v3.0.2 from v3.0.0. To address the error in resampling. The skimage.resize is included.


