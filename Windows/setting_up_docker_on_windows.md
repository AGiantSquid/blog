# Setting Up Docker On Windows

1. Make sure you are using Windows Pro.
Windows Home does not come with HyperV, and therefore cannot run Docker.
1. [Download Docker for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows).
1. Start Docker for Windows.
Click the box that says "Expose daemon on tcp://localhost:2375 without TLS."
1. [Install the Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) Choose Debian as your distro.<sup>[A](#blogSource)</sup>
1. Install all the debian things.
1. [Install Docker on Linux.](https://docs.docker.com/install/linux/docker-ce/debian/#install-using-the-repository)
The Docker Host daemon cannot run on WSL, only the client can.
You must run Docker for Windows to get an instance of Docker Host running, and then connect your Docker client in Linux from WSL.
1. Set up WSL to use `/` as your mount point for windows files instead of the default `/mnt`.
This is to ensure docker files mount properly when building a container.<sup>[B](#changeRootPath)</sup>
1. Clone your repo on the Windows filesystem, and run your docker commands from here as well.<sup>[C](#cloneRepo)</sup>
You do not need to duplicate the files to the WSL file system. (repo should be at  `/c/Users/[username]/[reponame]/)`.

#### footnotes
<a name="blogSource">A</a>: Install the Windows Subsystem for Linux

Open PowerShell as Administrator and run:
```PowerShell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
Restart your computer when prompted.
https://docs.microsoft.com/en-us/windows/wsl/install-win10


https://docs.docker.com/install/linux/docker-ce/debian/#install-using-the-repository

<a name="changeRootPath">B</a>: Setting Up Docker for Windows and WSL to Work Flawlessly
Create and modify the new WSL configuration file:
```bash
sudo nano /etc/wsl.conf
```
Now make the file look like the following:
```
[automount]
root = /
options = "metadata"
```
We need to set `root = /` because this will make your drives mounted at `/c`instead of `/mnt/c`.
Once you make those changes, sign out and sign back in to Windows to ensure the changes take effect. 

https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly

<a name="cloneRepo">C</a>: Clone the repo from within WSL or your line endings will all be messed up and your containers won't run. Run this if you have to first:

```bash
git config --global core.autocrlf false
```


All the debian things
```bash
sudo apt-get update
# install git
sudo apt-get install git-core
# generate an ssh key
ssh-keygen -t rsa
# add ssh to git

# clone any repos

# add Sublime Text https://www.sublimetext.com/docs/3/linux_repositories.html
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
sudo apt-get install apt-transport-https
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
sudo apt-get update
sudo apt-get install sublime-text

# add Sublime settings
cd ~/AddData/Roaming/Sublime\ Text\ 3/Packages/User/ 
git init
git remote add origin git@github.com:AGiantSquid/sublime_settings.git
git fetch
git reset --hard origin/master

# add meld
sudo apt-get install meld -y

# get dbus-x11 so sublime files open in same instance of sublime
sudo apt-get install dbus dbus-x11
```

Add the following to `.gitconfig`
```
[user]
	name = AGiantSquid
	email = ashley@greenkeytech.com
[diff]
    tool = meld
[difftool]
    prompt = false
[difftool "meld"]
    cmd = meld "$LOCAL" "$REMOTE"
[merge]
    tool = meld
[mergetool "meld"]
    cmd = meld "$LOCAL" "$BASE" "$REMOTE" --output "$MERGED"
    keepBackup = false
    prompt = false
[core]
	filemode = false
	autocrlf = false

```

And this for windows home directory `.gitconfig`
```
[user]
	email = ashley@greenkeytech.com
	name = AGiantSquid
[diff]
	guitool = meld
[difftool]
    prompt = false
[difftool "meld"]
    cmd = \"C:/Program Files (x86)/Meld/Meld.exe\" "$LOCAL" "$REMOTE"
[merge]
	tool = meld
[mergetool "meld"]
    cmd = \"C:/Program Files (x86)/Meld/Meld.exe\" "$LOCAL" "$BASE" "$REMOTE" --output "$MERGED"
    keepBackup = false
    prompt = false
[core]
	filemode = false
	autocrlf = false
```