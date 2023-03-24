![Alpine Banner](https://github.com/sttatusx/homelab/raw/main/os/alpine/banner.png)

# Alpine Server with Static IP and Docker Installation Guide

Alpine Linux is a lightweight and secure operating system, perfect for hosting Docker containers. With it's minimalist design and small footprint, Alpine is an excellent choice for those looking to maximize performance and efficiency.

<br />

## Installation

To install Alpine Linux, download the latest version of the ISO from the official website and follow the installation wizard. If you need help with this step, there are plenty of tutorials and videos online that can guide you through the process.

<br />

## Post-Installation Steps

After completing the installation, log in to the Shell environment using the user account that you created during installation. The first step is to update the system by running the following command:

<br />

```sh
$ sudo apk update && sudo apk upgrade
```


<br />

## Configure a Static IP Address

To set a static IP address for your Alpine server, follow these steps:

1. Open the `/etc/network/interfaces` file using your preferred text editor.
2. Locate the network interface you want to configure (e.g., `eth0` or `enp0s3`).

<br />

> You can find the network interface by running `ip addr show`

<br />

3. Add the following lines to the interface configuration block:

```yaml
auto <interface-name>
iface <interface-name> inet static
    address <desired-IP-address>
    netmask <subnet-mask>
    gateway <default-gateway-IP-address>
```

Be sure to replace `<interface-name>`, `<desired-IP-address>`, `<subnet-mask>`, and `<default-gateway-IP-address>` with the appropriate values for your network.

<br />

4. Save the changes to the `/etc/network/interfaces` file.
5. Restart the networking service with the command:

```sh
$ sudo service networking restart
```

<br />

After completing these steps, your Alpine Linux server should be configured with a static IP address.

<br />

## Change the Default SSH Port
Changing the default SSH port number is an essential step in improving the security of your server and making it less vulnerable to automated attacks. Here's how you can do it:

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
4. Restart the `ssh` and `sshd` services by running the following command:

```sh
$ sudo service sshd restart
```

<br />

5. Verify that the new SSH port is working by opening a new terminal window and running the following command, replacing `username` and `server_ip_address` with your own values:

```sh
$ ssh -p 2222 username@server_ip_address
```

<br />

## Install Docker

Docker is a popular platform for developing, shipping, and running applications in containers. Here's how you can install Docker on Alpine Linux:

```sh
$ sudo apk add docker docker-compose
```

<br />


After installing Docker, you can start the Docker service on Alpine startup by running the following commands:

```sh
$ sudo rc-update add docker boot
$ sudo service docker start
```

<br />


It's also recommended to add your user account to the `docker` group, so you can run Docker commands without using `sudo`. You can do this with the following command:

```sh
$ sudo addgroup $USER docker
```
