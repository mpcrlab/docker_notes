# Install Docker

These commands should be run in the terminal on Ubuntu.
If these instructions, don't work, run the commands from [here](https://docs.docker.com/install/linux/docker-ce/ubuntu/) or google "install docker ce ubuntu".

1. Update and make sure `curl` is installed to download the install script.
```Bash
sudo apt-get update
sudo apt-get install -y curl
```

2. Download and run the Docker install script.
```Bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

3. add the current user to the "docker" group, so we can run commands without `sudo`
```Bash
sudo usermod -aG docker $(whoami)
```
# Install CUDA Driver (Required to use GPUs)

Only do this part if you don't already have a CUDA driver installed.

0. Check if you have a CUDA driver already installed by running `nvidia-smi` in the terminal. If the command outputs something like this, you can skip the rest of this section.
```Shell Session
mpcrpaul@mpcrpaul-MS-7B61:~$ nvidia-smi
Wed Feb 19 21:20:21 2020       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 418.56       Driver Version: 418.56       CUDA Version: 10.1     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 108...  Off  | 00000000:01:00.0  On |                  N/A |
| 23%   36C    P8    18W / 250W |   8819MiB / 11177MiB |      5%      Default |
+-------------------------------+----------------------+----------------------+
|   1  GeForce GTX 108...  Off  | 00000000:03:00.0 Off |                  N/A |
| 23%   28C    P8     8W / 250W |   7589MiB / 11178MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1179      G   /usr/lib/xorg/Xorg                           205MiB |
|    0      2564      G   compiz                                       231MiB |
|    0      3008      G   /usr/lib/firefox/firefox                       2MiB |
|    0      3189      G   /opt/teamviewer/tv_bin/TeamViewer              9MiB |
|    0      5440      G   ...quest-channel-token=7951824858324179070   107MiB |
|    0     10535      G   /usr/lib/firefox/firefox                       2MiB |
|    0     23424      C   /usr/bin/python3                            8251MiB |
|    0     23478      G   /usr/lib/firefox/firefox                       2MiB |
|    1     23424      C   /usr/bin/python3                            7577MiB |
+-----------------------------------------------------------------------------+
```

1. Add this 3rd party NVIDIA graphics drivers repository
```Bash
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt-get update
```

2. List the available drivers by running `ubuntu-drivers devices`. Output should look something like this (Note the driver versions):
```Shell Session
mpcrpaul@mpcrpaul-MS-7B61:~$ ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0 ==
vendor   : NVIDIA Corporation
modalias : pci:v000010DEd00001B06sv000010DEsd0000120Fbc03sc00i00
driver   : nvidia-384 - distro non-free
driver   : nvidia-430 - third-party free recommended
driver   : nvidia-410 - third-party free
driver   : nvidia-415 - third-party free
driver   : nvidia-418 - third-party free
driver   : xserver-xorg-video-nouveau - distro free builtin
```

3. Install the graphics driver version you want (i.e. `nvidia-418`). Try the most recent one if you're not sure, and downgrade if that breaks anything. Compatibility between driver versions and CUDA Toolkit versions can be found in [this table](https://docs.nvidia.com/deploy/cuda-compatibility/index.html#binary-compatibility__table-toolkit-driver).
```Bash
sudo apt-get install nvidia-[VERSION]
```

4. Restart your computer, and `nvidia-smi` should work.
```
sudo reboot
```
