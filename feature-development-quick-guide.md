# Feature Development Quick Guide

## Intro

This guide will give a brief oveview on how to get started developing LinuxGSM by running though some of the basics of using GitHub and the tools you need. This is not a comprihensive guide to GitHub but should help with getting started. There are plenty of resources available online such as the [GitHub help documentation](https://help.github.com/en/github) that will help you learn more.

## Requirements

Before you get started a few tools are required for development. The tools used are down to the developers preferences. However there are some reccomendations if you are new.

### GitHub Account

LinuxGSM uses GitHub to host the code, becuase of this a github account is required.

### Text editor

LinuxGSM is written in BASH and can be developed simply by using a text editor. The reccomended text editor is Atom as it is Open Source and is developed by GitHub so has some great integrations. However if a developer is more comfortable with another editor that is fine.  For specific requirements for text editors see [Text Editor Settings](text-editor-settings.md).

* [Atom \(](https://atom.io/)recommended\)
* [Sublime Text](https://www.sublimetext.com/)
* [Notepad++](https://notepad-plus-plus.org/)

### Git Client

To edit code, create branches and submit Pull Requests a Git client is required to work on the project. The reccomended Git client is Git Kracken as it is feature rich and easy to understand the branch relationships.  Atom also has a built in Git Client which is useful for beginners. Both Git Kracken and Atom integrate well with GitHub.

* [GitKracken](https://www.gitkraken.com/) \(recommended\)
* [Atom](https://atom.io/)
* [Github Desktop](https://desktop.github.com/)

### SSH Client

To connect to Linux servers an SSH client is needed. There are various clients available to choose from. For Windows MobaXterm is a great option or the classic PuTTY. For Linux and Mac Remmina works well for saving SSH sessions.

* [MobaXterm](https://mobaxterm.mobatek.net/) \(Windows\)
* [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) \(Windows\)
* [Remmina](https://remmina.org/) \(Linux & Mac\)

### Test Enviroment

LinuxGSM runs on Linux and as such requires a Linux enviroment for development and testing. Most developers will be running Windows but there are multiple ways to create a Linux development enviroment.

#### Distro

LinuxGSM is primarily developed on Ubuntu but also tested to work on CentOS and Debian. Different versions of a distro will also have different versions of BASH etc. So bein mindful of newer feature that might not be available on older supported distros. In general LinuxGSM will support distros that are still officialy supported by the vendor but is also reliant on if the Game Server also supports the distro. See [distro](https://docs.linuxgsm.com/linux/distro) for more info.

#### Virtual Machine

Creating a virtual machine on a desktop or laptop is a good way to create a development enviroment. Using Virtual Box and downloading Ubuntu Server iso a test enviroment can be created quickly. However to test internet functionality there may be a requirement to open ports on a home router.

If spare computer hardware is available, setting up an ESXi or Xen Server may be a good option for a development enviroment.

* [Virtual Box](https://www.virtualbox.org/) \(reccomended\)
* [VMware Player](https://www.vmware.com/uk/products/workstation-player.html)
* [ESXI Server](https://www.vmware.com/uk/products/esxi-and-esx.html)
* [Xen](https://xenproject.org/)
* [Proxmox](https://www.proxmox.com/)

#### Internet Server

VPS and dedicated servers can be rented relativly cheaply and is a good way to test LinuxGSM in the enviroment it is mostly used \(online\). There are several providers like Linode that provide servers from $5 p/m and allow the quick deployment of servers with different distros. Some game servers do have higher system requires than others so a more powerful VPS may be required.

There are many providers to choose from but below LinuxGSM developers have used previously.

* [Linode](https://linode.com/)
* [Digital Ocean](https://www.digitalocean.com/)
* [Oneprovider](https://oneprovider.com/)
* [Kimsufi](https://www.kimsufi.com/)

## Chosing an Issue to Develop

Whenever someone raises new feature reques or bug is done on the [GitHub Issues](https://github.com/GameServerManagers/LinuxGSM/issues) page. There are a raft of issues with different levels of complexity. Choosing an issue to work on is down to you as an individual, however it is important you enjoy working on it. It is reccomended that a simple issues is picked first and more complex issues are attempted as you get used to LinuxGSM. Popular issues to attempt are [`type:Server Requests`](https://github.com/GameServerManagers/LinuxGSM/issues?q=is%3Aissue+is%3Aopen+label%3A%22type%3A+server+request%22) as often developers want to have a game server added to the project. Be warned however some game servers can be more difficult than others to develop.

To help filter issues GitHub uses [labels](https://help.github.com/en/github/managing-your-work-on-github/about-labels) to help identify the types of issues. Common labels include `type:bug`,`type:feature`,`command:monitor`,`game: 7 Days to Die`. Labels are split in to label types such as `type`, `command`, `game`, `info` etc to assist in triage.

## Starting Development

To begin working on LinuxGSM you need to [fork](https://help.github.com/en/github/getting-started-with-github/fork-a-repo) the LinuxGSM repository once forked you will need to [clone](https://help.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository-from-github) your new repository to your local machine using yourchoosen git client. Once cloned it is possible to edit the code on your local machine using your text editor of choice. 

It is reccomended you create a [branch](branching.md) to develop your code. The branch should use the Gitflow methodology and should be named `feature/[featurename]`.

Once a change has been made and saved the change will need to be commited to your local repo. When using commit it is important to leave a useful message to describe the change, this is covered in [Conventional Commits](conventional-commits.md). When you are ready to send your commits to your remote fork you will need to [push ](https://help.github.com/en/github/using-git/pushing-commits-to-a-remote-repository)the updates.

## Using the Test Enviroment

At some point you will need to test the code you have worked on. This can be done by downloading LinuxGSM and updating the repo and branch details to match your fork.

#### Setup Testing Enviroment

Login to your develop enviroment and begin installing LinuxGSM 

 1. Create a user and login.

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

3. Rename the github username, repo and branch to match you one you are developing on.

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

#### Updating the Test Enviroment

Everytime you push to remote it is possible to pull the changes to the test enviroment. This is done by using the development command `clear-functions`.

To use clear-functions activate development mode.

```bash
./gameserver development
```

Run the command.

```bash
./gameserver clear-functions
```

## Create a Pull Request

Once the code you have worded on is ready to be submitted to the LinuxGSM project a [pull request](branching.md) will need to be raised. Pull requests have a list of things that need to be completed to get it merged in to the project. Follow these steps as much as possible to ensure that your code can be merged quicker. When the pull request is raised various unit tests will be done on the code to ensure it follows the correct standards. When naming a pull request ensure that it following [Conventional Commits](https://www.conventionalcommits.org/) standards. As this is what is used for generating the [changelog](https://github.com/GameServerManagers/LinuxGSM/releases) for the next release. 

A best practice for writing a commit message is to say in your head the following, followed by the change you are making.

> If I commit this change it will......._add slack support to alerts_

```bash
feat(alerts): add slack support to alerts
```

```bash
fix(csgoserver): remove SteamCMD auth requirement 32-bit workaround 
```

Once the Pull Request is created it is now time to wait. The Pull Request will need be reviewed by LinuxGSM developers who regularly work on the project. They will accept, reject or reccomend changes to the Pull Request. This can take time or your pull request will be held until a time that is appropriate to merge in to the project so please be patient. One of the developers may leave a comment to make changes or make changes themselves to make the commit ready. Once this review proccess is completed  congratulations your commit will be merged ready for the next release.

