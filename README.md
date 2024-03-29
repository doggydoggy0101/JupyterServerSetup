# JupyterServerSetup
setup CUDA environment &amp; Jupyter notebook remote server for windows

## For windows!!!

* [ CUDA environment ](#cuda)
* [ Router settings ](#router)
* [ Jupyter notebook server ](#server)
* [ Environments ](#conda)
* [ side-issues](#issue)
* [ others](#other)

**Anaconda**\
https://www.anaconda.com/download

<a name="cuda"></a>
## CUDA environment

**Nvidia driver** (normally built-in)\
https://www.nvidia.com.tw/Download/index.aspx?lang=en

**CUDA toolkit**\
https://developer.nvidia.com/cuda-toolkit-archive

download version CUDA 11.7 for pytorch compatibility (latest version should work too)

<img src="https://github.com/doggydoggy0101/JupyterServerSetup/blob/main/pytorch.png" alt="image" width="800"/>

check CUDA environment after installation:

```shell
nvcc -V
```

**cuDNN**\
https://developer.nvidia.com/rdp/cudnn-archive

download version that is compatibe with CUDA 11.7 (or the CUDA version you installed),\
copy contents in ```bin/include/lib``` to the folders respectively, path is ```C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.7```

**Pytorch with CUDA**\
https://pytorch.org/get-started/locally/

as mentioned above, install pytorch+CUDA 11.7 with pip:

```shell
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu117
```

**check!**
```python
import torch
print(torch.cuda.is_available())
# print(torch.cuda.get_device_name(0))
```


<a name="router"></a>
## Router settings
**static IP address**\
check the information of your static IP address by the following steps:


1. win+R type ncpa.cpl
2. right click ```<yourEthernet>``` properties
3. double click Internet Protocol Version 4 (TCP/IPv4) 

Copy all the information of the IP address here, set it to automatically obtain IP address afterwards.

**Router**

1. set up your router with your static IP address

2. assign a specific IP for your device from DHCP IP reservation\
   (routers assign dynamic IP addresses for devices by default, setting a specific IP address is necessary for port fowarding)

3. set up a specific port for your device's IP from NAT/port fowarding setting\
   (the specific IP above, use the same port for external and internal port just for simplicity)

Now ```<staticIPaddress>:<specificPort>``` should connect to your device, where ```<staticIPaddress>``` is the connection to your router and ```<specificPort>``` is the connection from your router to your device. 

Remember to change your device to automatically obtain IP address from where you check the IP information.


<a name="server"></a>
## Jupyter notebook server
jupyter notebook should be installed with anaconda

```shell
### set a password
jupyter notebook password
```

**host jupyter notebook**\
host with IP 0.0.0.0, local machine use localhost or 127.0.0.1, others use ```<staticIPaddress>```, port is the ```<specificPort>```

```shell
jupyter notebook --no-browser --ip 0.0.0.0 --port <specificPort>

### local machine
127.0.0.1:<specificPort>
### others
<staticIPaddress>:<specificPort>
```

<a name="conda"></a>
### Environments
**conda environments**
```shell
### create new environment
conda create --name <envName> python=<pythonVersion>
conda activate <envName>
conda deactivate

### manage conda environments
conda env list
conda remove --name <envName>  --all
```
**jupyter notebook kernels**
```shell
### create new kernel
conda activate <envName>
(envName)$ pip install jupyter
(envName)$ ipython kernel install --name "<kernelName>"

### manage jupyter kernels
jupyter kernelspec list
jupyter kernelspec remove <kernelName>
```


<a name="issue"></a>
### side-issues
got an error after ctrl+C while training, upgrading scipy should work
```shell
pip install --upgrade scipy
```
---
jupyter notebook uses powershell by default, but powershell may not work with conda environment
```
jupyter notebook --generate-config
```
then go to config located at ```<user>/.jupyter/jupyter_notebook_config.py``` and change it to cmd
```
c.NotebookApp.terminado_settings = {
    'shell_command': ['C:\\Windows\\System32\\cmd.exe']
}
```
---
set up remote desktop by port 3389


<a name="other"></a>
### others

linux conda install

https://jscinin.medium.com/linux-ubuntu-%E7%B3%BB%E7%B5%B1%E4%B8%8B%E5%AE%89%E8%A3%9D-anaconda-be5021ff4cd2

linux conda path

https://blog.csdn.net/weixin_38705903/article/details/86533863

wsl with VcXsrv gui

https://hackmd.io/@JYU/B1zmv1MCU

