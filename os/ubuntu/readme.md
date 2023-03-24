# Ubuntu Server with Static IP and Docker Installation Guide

If you're setting up a home lab or a development environment, Ubuntu Server is a great choice due to its ease of use and popularity. In this guide, we'll go through the steps required to install Ubuntu Server, configure a static IP address, and install Docker.

<br />

## Installation

To install Ubuntu Server, download the latest version of the ISO from the official website and follow the installation wizard. If you need help with this step, there are plenty of tutorials and videos online that can guide you through the process.

<br />

## Post-Installation Steps

After completing the installation, log in to the Shell environment using the user account that you created during installation. The first step is to update the system by running the following command:

<br />

```sh
$ sudo apt-get update && sudo apt-get upgrade
```

<br />

### Internet Connection Issues

If you're unable to access the internet after installing Ubuntu, the issue may be with the `netplan` package. You can modify the netplan configuration file located at `/etc/netplan/SOME_CONFIG.yml` to fix the issue.

<br />

## Configure a Static IP Address

To set a static IP address for your Ubuntu server, follow these steps:

1. Open the netplan configuration file by running the following command:

```sh
$ sudo nano /etc/netplan/01-netcfg.yaml
```

<br />

2. Add the following lines to the file, replacing the `IP address`, `gateway`, and `DNS server` values with your own:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3: # Replace with the name of your network interface
      addresses:
        - 192.168.0.10/24 # Replace with your desired IP address and subnet mask
      gateway4: 192.168.0.1 # Replace with your router's IP address
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4] # Replace with your DNS server addresses
```

> You can find the network interface by running `ip addr show`

<br />

3. Save and close the file.
4. Apply the changes by running the following command:

```sh
$ sudo netplan apply
```

<br />

## Change the Default SSH Port
Changing the default SSH port number is an essential step in improving the security of your Ubuntu server and making it less vulnerable to automated attacks. Here's how you can do it:

<br />

1. Open the `sshd_config` file by running the following command:

```sh
$ sudo nano /etc/ssh/sshd_config
```

<br />

2. Uncomment the `#Port 22` line and change the port number to something else, like `2222`.

```
Include /etc/ssh/sshd_config.d/*.conf

Port 2222
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::
```

<br />

3. Save and close the file.
4. Restart the `ssh` and `sshd` services by running the following commands:

```sh
$ sudo systemctl restart ssh
$ sudo systemctl restart sshd
```

<br />

5. Allow the new port in the UFW firewall:

```sh
$ sudo ufw allow 2222
```

> This will open the new SSH port `2222` on your Ubuntu server's firewall.

<br />

6. Verify that the new SSH port is working by opening a new terminal window and running the following command, replacing `username` and `server_ip_address` with your own values:

```sh
$ ssh -p 2222 username@server_ip_address
```

<br />

## Install Docker

Docker is a popular platform for developing, shipping, and running applications in containers. Here's how you can install Docker on Ubuntu Server:

> Follow this guide from the official Docker documentation to install Docker on Ubuntu: https://docs.docker.com/engine/install/ubuntu/

<br />


After installing Docker, you can start the Docker service on Ubuntu startup by running the following command:

```sh
$ sudo systemctl enable --now docker
```

<br />


It's also recommended to add your user account to the `docker` group, so you can run Docker commands without using `sudo`. You can do this with the following command:

```sh
$ sudo usermod -aG docker $USER
```

