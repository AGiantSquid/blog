# Setting Up Docker On Windows

Make sure you are using Windows Pro. Windows Home does not come with HyperV, and therefore cannot run Docker.
Download Docker for Windows.
Start Docker for Windows. Click the box that says "Expose daemon on tcp://localhost:2375 without TLS."
Enable the Windows Subsystem for Linux. Choose Debian as your distro.
Install Docker on Linux. The Docker Host daemon cannot run on WSL, only the client can. You must run Docker for Windows to get an instance of Docker Host running, and then connect your Docker client in Linux from WSL.
Set up WSL to use / as your mount point for windows files instead of the default /mnt. This is to ensure docker files mount properly when building a container.A
Clone your repo on the Windows filesystem, and run your docker commands from here as well.B
- You do not need to duplicate the files to the WSL file system. (repo should be at  /c/Users/[username]/[reponame]/).





A. Create and modify the new WSL configuration file:
https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly

sudo nano /etc/wsl.conf
Now make the file look like the following:

[automount]
root = /
options = "metadata"
We need to set root = / because this will make your drives mounted at /c or /e instead of /mnt/c and /mnt/e.
Once you make those changes, sign out and sign back in to Windows to ensure the changes take effect. 



B. Clone the repo from within WSL or your line endings will all be messed up and your containers won't run. Run this if you have to first:

git config --global core.autocrlf false

