# Test Environment

LinuxGSM runs on Linux \(obviously\) and as such requires a Linux test environment to test game servers and code. If you are running a LInux desktop then you can run LinuxGSM using your desktop. However, Most developers will be running Windows but there are multiple ways to create a Linux test environment.

## Selecting a Test Environment

There are mulitple ways to setup a test enviroment.

### Distro

LinuxGSM is primarily developed on Ubuntu but also tested to work on CentOS and Debian. Different versions of a distro will also have different versions of BASH etc. So be mindful of newer features that might not be available on older supported distros. In general, LinuxGSM will support distros that are still officially supported by the vendor but is also reliant on if the Game Server also supports the distro. See [distro](https://docs.linuxgsm.com/linux/distro) for more info.

### Virtual Machine

Creating a virtual machine on a desktop or laptop is a good way to create a development environment. Using Virtual Box and downloading Ubuntu Server iso a test environment can be created quickly. However, to test internet functionality there may be a requirement to open ports on a home router.

If spare computer hardware is available, setting up an ESXi or Xen Server may be a good option for a development environment.

* [Virtual Box](https://www.virtualbox.org/) \(recommended\)
* [VMware Player](https://www.vmware.com/uk/products/workstation-player.html)
* [ESXI Server](https://www.vmware.com/uk/products/esxi-and-esx.html)
* [Xen](https://xenproject.org/)
* [Proxmox](https://www.proxmox.com/)

### Internet Server

VPS and dedicated servers can be rented relatively cheaply and is a good way to test LinuxGSM in the environment it is mostly used \(online\). There are several providers like Linode that provide servers from $5 p/m and allow the quick deployment of servers with different distros. Some game servers do have higher system requires than others so a more powerful VPS may be required.

There are many providers to choose from but below LinuxGSM developers have used previously.

* [Linode](https://linode.com/)
* [Digital Ocean](https://www.digitalocean.com/)
* [Oneprovider](https://oneprovider.com/)
* [Kimsufi](https://www.kimsufi.com/)



At some point, you will need to test the code you have worked on. This can be done by downloading LinuxGSM and updating the repo and branch details to match your fork. 

Login to your development environment and begin installing LinuxGSM

#### Setup Testing Environment

Login to your develop environment and begin installing LinuxGSM.

 1. Create a user and log in.

```text
adduser linuxgsm
```

```text
passwd linuxgsm
```

```text
su - linuxgsm
```

> replace `[gameserver]` with the game server you are developing.

```bash
mkdir [gameserver] 
```

2. Download linuxgsm.sh.

```bash
wget -O linuxgsm.sh https://linuxgsm.sh && chmod +x linuxgsm.sh
```

3. Rename the GitHub username, repo and branch to match you one you are developing on.

```bash
## GitHub Branch Select
# Allows for the use of different function files
# from a different repo and/or branch.
githubuser="GameServerManagers"
githubrepo="LinuxGSM"
githubbranch="master"
```

4. Install the game server

```bash
./linuxgsm install
```

#### Updating the Test Environment

Every time you push to remote it is possible to pull the changes to the test environment. This is done by using the development command `clear-functions`.

To use clear-functions activate development mode.

```bash
./gameserver development
```

Run the command.

```bash
./gameserver clear-functions
```

