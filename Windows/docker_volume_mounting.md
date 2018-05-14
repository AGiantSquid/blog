Fix for this error:

C:\Program Files\Docker\Docker\Resources\bin\docker.exe: Error response from daemon: Mount denied:
The source path "C:/Users/some/path/files/;C"
doesn't exist and is not known to Docker.
See 'C:\Program Files\Docker\Docker\Resources\bin\docker.exe run --help'.
If you are using Windows with Git Bash (or some other console emulator), and want to use interpolation with pwd for a file path, you need an extra slash at the beginning of the file path.

So, instead of this:

-v $(pwd)/uploads:/uploads \ 

do this:

-v /$(pwd)/uploads:/uploads \

E.g. 

docker run --rm -d \
  -p 8082:5000 \
  -v /$(pwd)/uploads:/uploads \
  -v /$(pwd)/files:/files \
  containername

If using Windows Subsystem for Linux (WSL), it is important to note that you must access a file from the Windows file system, not from the WSL Linux file system. Docker is running on Windows, and so it only has access to the Windows filepath. 

Do not clone the repo into WSL, just navigate to the repo in your windows filesystem.

You must set up WSL to mount windows file systems to / instead of the default, which is /mnt for the $(pwd) command to work. https://nickjanetakis.com/blog/setting-up-docker-for-windows-and-wsl-to-work-flawlessly
