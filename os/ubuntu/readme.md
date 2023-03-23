# Ubuntu Server
I chose the Ubuntu Server distribution to start setting up my home lab, and I have no regrets about this choice so far. Ubuntu has done most of the hard work for you, and you can just focus on setting up your home server without any hassle.

These were the steps I followed to configure my Ubuntu server. Here, I tried to write down all the steps without depending on the previous step and with complete explanations.


<br />

## Goal
After completing all of these steps, you will have an Ubuntu server with a static IP address, as well as Docker installed and ready to use.

<br />

## Installation
Just google it! it's that easy!  


<br />

## Post Installation
After completing the Ubuntu installation, you can log in to the Shell environment using the user account that you created during installation. From there, you can update your system by entering the command below:

<br />

```sh
$ sudo apt-get update && sudo apt-get upgrade
```

<br />

### Internet Problem
The `netplan` package is responsible for managing network connections in Ubuntu. If you are unable to access the internet after installing Ubuntu, you may need to modify the netplan configuration file located at `/etc/netplan/SOME_CONFIG,yml`.  


<br />

## Static IP


<br />

## Changing Default SSH Port

```sh
$ sudo vim /etc/ssh/sshd_config
```

Restart the `ssh` service

```sh
$ sudo systemctl restart ssh
```


### Add new port to the firewall

<br />

## Installing Docker


### Add Docker to the user groups

```sh
$ sudo usermom -aG docker $USER
```