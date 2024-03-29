# **WSL2 | Docker | Minikube instalation**

## WSL2

[GitHub page](https://kselnaag.github.io/cheatsheet_WSL2_Docker_Minikube "GitHub page")

First of all you should deactivate `Hyper-V` service and activate `WSL2` service into your windows system. Use `PowerShell` in admin mode:
```Power Shell
Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-Hypervisor
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
Or just do it like this:

<p align="center">
  <img src="https://raw.githubusercontent.com/kselnaag/WSL2_Docker_Minikube_inst/gh-pages/WSL.png" alt="Programms and components"/>
</p>

Next go to `cmd` console, update `WSL` up to 2-nd version and use some commands for instalation Linux system on `WSL2`:
```CMD
wsl --status
wsl --update
wsl --set-default-version 2
wsl --list --verbose
wsl --list --online
wsl --install -d Ubuntu-20.04     # wsl --unregister Ubuntu-20.04 (delete OS)
wsl --set-default Ubuntu-20.04    # wsl --shutdown (reboot wsl system)
```
#### Official Microsoft mans:
[Hyper-V disable](https://docs.microsoft.com/ru-ru/troubleshoot/windows-client/application-management/virtualization-apps-not-work-with-hyper-v) | 
[WSL Enabled](https://docs.microsoft.com/ru-ru/windows/wsl/install-on-server) | 
[WSL manual](https://docs.microsoft.com/ru-ru/windows/wsl/install-manual) | 
[WSL basic comands](https://docs.microsoft.com/ru-ru/windows/wsl/basic-commands) 

Now Ubuntu-20.04 installed on your WSL2 service.

## Docker

Start `bash` in linux you've just installed and tune the system first. After you should work with `apt-get` to clean the old packets (*just in case*), install some utility packets and get new packets from docker repo.
```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
sudo apt-get update
sudo apt-get -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get -y install docker-ce
docker version
sudo usermod -aG docker $USER
sudo service docker start
sudo update-rc.d docker enabled
service --status-all
docker run --rm hello-world
```
[Docker official man](https://docs.docker.com/engine/install/ubuntu/)

Make sure  that console shows you correct info about docker version, docker-service status and the container named `hello-world` run successfully.

## Minikube

Now we can download latest build for your system and install minikube. Check the [Minikube official man](https://minikube.sigs.k8s.io/docs/start/) first and type something like that:
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
minikube version
minikube start
```
Make sure that Minikube has latest version and runs correctly.

Then you can install and tune `kubectl` manualy or get it from minikube dirrectly:
```bash
minikube kubectl -- get po -A
minikube kubectl version
```

## Optional

You can use you favorite text editor or CLI and do some optimizations:
```bash
nano ~/.bashrc
+alias d='docker'
+alias k='minikube kubectl --'
source ~/.bashrc
```
or
```bash
echo -e "alias d='docker'\nalias k='minikube kubectl --'" >> ~/.bashrc
source ~/.bashrc
```
Install `ssh`, `git`, `helm`, `ansible` and so on to be a cool computer guy. 
______

`WSL2`, `Docker` and `Minikube` installed on local machine for your experiments !

#### Links:
[Hyper-V disable](https://docs.microsoft.com/ru-ru/troubleshoot/windows-client/application-management/virtualization-apps-not-work-with-hyper-v) | 
[WSL Enabled](https://docs.microsoft.com/ru-ru/windows/wsl/install-on-server) | 
[WSL manual](https://docs.microsoft.com/ru-ru/windows/wsl/install-manual) | 
[WSL basic comands](https://docs.microsoft.com/ru-ru/windows/wsl/basic-commands) | 
[Docker official man](https://docs.docker.com/engine/install/ubuntu/) | 
[Minikube official man](https://minikube.sigs.k8s.io/docs/start/) 
