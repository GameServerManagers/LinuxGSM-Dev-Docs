# Test Environment

LinuxGSM is designed to run on Linux, and therefore, a Linux test environment is essential for testing game servers and code changes. Whether you're already using a Linux desktop or primarily work on Windows, there are multiple ways to create a suitable Linux test environment. Additionally, if you are using Windows, you can leverage Windows Subsystem for Linux (WSL) to streamline your development process.

## Distro

LinuxGSM is primarily developed on Debian-based distros but is also tested to work on RedHat-based distros. Keep in mind that different distributions and versions may have varying versions of BASH and other dependencies. Ensure that your chosen distribution is still officially supported by the vendor and that it's compatible with the game server you intend to work with.

## Selecting a Test Environment

### **Using a Linux Desktop**

If you're already using a Linux desktop, you can run LinuxGSM directly on your desktop environment. This approach simplifies the setup process since LinuxGSM is natively compatible with Linux distributions.

### **Windows with WSL**

For developers using Windows, Windows Subsystem for Linux (WSL) provides an efficient way to create a Linux test environment without dual-booting or using virtual machines. You can install a Linux distribution of your choice via WSL and then proceed to set up LinuxGSM within that distribution.

### Virtual Machine

Creating a virtual machine on your desktop or laptop is a versatile way to create a development environment. You can use tools like VirtualBox to download an Ubuntu Server ISO and quickly set up a test environment. Note that for testing internet functionality, you may need to configure port forwarding on your home router.

-   [Virtual Box](https://www.virtualbox.org/)
-   [VMware Player](https://www.vmware.com/uk/products/workstation-player.html)
-   [ESXI Server](https://www.vmware.com/uk/products/esxi-and-esx.html)
-   [Xen](https://xenproject.org/)
-   [Proxmox](https://www.proxmox.com/)

### Internet Server

Renting a virtual private server (VPS) or dedicated server can be an excellent choice for testing LinuxGSM in an online environment, which closely resembles how it's commonly used. Several providers offer cost-effective server options, making it accessible for testing purposes.

Notable providers include:

-   [Linode](https://linode.com/)
-   [Digital Ocean](https://www.digitalocean.com/)
-   [OVHCloud](https://ovhcloud.com)
-   [Oneprovider](https://oneprovider.com/)
-   [Kimsufi](https://www.kimsufi.com/)

## **Testing Your Code**

At some point, you will need to test the code you have worked on. This can be done by downloading LinuxGSM and updating the repo and branch details to match your fork.

### Setup Testing Environment

Login to your development environment and begin installing LinuxGSM.

1. Create a user and log in.

```bash
adduser linuxgsm
```

```bash
passwd linuxgsm
```

```bash
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

To use clear-modules activate development mode.

```bash
./gameserver development
```

Run the command.

```bash
./gameserver clear-modules
```
