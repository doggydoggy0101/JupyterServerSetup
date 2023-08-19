# JupyterServerSetup
setup CUDA environment &amp; Jupyter notebook remote server for windows

## For windows!!!

* [ CUDA environment ](#cuda)
* [ Jupyter notebook server ](#server)
* [ side-issues](#issue)

**Anaconda**\
https://www.anaconda.com/download

<a name="cuda"></a>
### CUDA environment

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
copy contents in bin/include/lib to the folders respectively, path:

```
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.7
```

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

<a name="server"></a>
### Jupyter notebook server
jupyter notebook should be installed with anaconda

```shell
### set a password
jupyter notebook password
### get your ip address
ipconfig
```

**host jupyter notebook**\
host with IP 0.0.0.0, local machine use localhost or 127.0.0.1, others use \<yourIPaddress>, port doesn't matters

```shell
jupyter notebook --no-browser --ip 0.0.0.0 --port 8888

### local machine
127.0.0.1:8888
### others
<yourIPaddress>:8888
```

<a name="issue"></a>
### side-issues
got an error after ctrl+C while training, upgrading scipy should work
```shell
pip install --upgrade scipy
```
