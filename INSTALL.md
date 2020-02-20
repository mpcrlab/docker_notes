# Install Docker

These commands should be run in the terminal on Ubuntu.

1. Update and make sure `curl` is installed to download the install script.
```
sudo apt-get update
sudo apt-get install -y curl
```

2. Download and run the Docker install script.
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

3. add the current user to the "docker" group, so we can run commands without "sudo"
```
sudo usermod -aG docker $(whoami)
```
