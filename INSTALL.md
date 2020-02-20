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


