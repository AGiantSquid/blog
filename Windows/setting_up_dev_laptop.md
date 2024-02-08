# install VSCode
    - install extensions:
        - python
        - remote development
        
# install useful programs
    - vlc
    - obs studio

# install wsl2

Open powershell with admin priveledges and run:

`wsl --install -d debian`

# update linux os
```shell
sudo apt-get update
```

# Create and modify the new WSL configuration file to prevent `/mnt` directory
```shell
sudo nano /etc/wsl.conf
```
Add the following:
```
[automount]
root = /
options = "metadata"
```

Sign out and in again (do not just lock the screen, actually log out).

# change home dir permission to 700 (or ssh won't work)
```shell
cd
chmod 700 .
```

# install needed programs
```
sudo apt-get install openssh-server -y
sudo apt-get install git-all -y
```

# generate ssh keys
```shell
ssh-keygen
```

# make sure .ssh file and contents have correct permissions
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_rsa
chmod 644 ~/.ssh/id_rsa.pub
```

# later, update these files too: 
```shell
chmod 644 ~/.ssh/authorized_keys
chmod 644 ~/.ssh/known_hosts
chmod 644 ~/.ssh/config
```

# add new ssh keys to github

# install dotfiles config

https://github.com/AGiantSquid/myconfig/tree/master/.myconfig

# install python 

https://github.com/AGiantSquid/blog/blob/master/Windows/setup_python.md

![image](https://github.com/AGiantSquid/blog/assets/26531374/20e78e0f-bf35-48e7-899f-973881d01daa)

# setup ssh to run on port 2222
Port 22 is taken by Windows
```shell
sudo nano /etc/ssh/sshd_config
```
change `#Port 22` to `Port 2222`

make sure:
```
PermitRootLogin no
ListenAddress 0.0.0.0
AllowUsers [username]
PubkeyAuthentication yes
PasswordAuthentication yes
```

# start ssh server

```shell
sudo service ssh start
```

# open port 2222 in windows
```
Click Start
Type Windows Firewall.

Click Windows Firewall.
Click Advanced settings.

Click Inbound Rules. Click New Rule.
Click Port.
Click Next.

Click TCP.
Click Specific local ports.

Type a port number. (In this case, we will open port 2222.)
Click Next.

Click Allow the connection. 
Click Next.

Click any network types you'd like to allow the connection over. (Domain, Private)
Click Next.

Type a name for the rule. (WSL)
Click Finish.
```

# create script in windows 

sshd.bat
```
@echo off
setlocal

C:\Windows\System32\bash.exe -c "sudo /usr/sbin/service ssh start"

netsh interface portproxy delete v4tov4 listenport=2222 listenaddress=0.0.0.0 protocol=tcp

for /f %%i in ('wsl hostname -I') do set IP=%%i
netsh interface portproxy add v4tov4 listenport=2222 listenaddress=0.0.0.0 connectport=2222 connectaddress=%IP%

endlocal
```

# run the script

`.\sshd.bat`

# get ipv4 address of windows server 

Click internet settings. Get IPv4 address (probably 192.168.x.xx)

# make sure network is set to be discoverable

![image](https://github.com/AGiantSquid/blog/assets/26531374/02d9c3f3-7356-4b9d-9648-b552d598a0f2)


# verify ssh works

`ssh 192.168.x.xx -p 2222`

# add keys to dev machine from other computer
```shell
ssh-copy-id -i ~/.ssh/id_rsa.pub [username]@192.168.1.xxx -p 2222
```
(you'll have to type password)

# add keys to dev machine from windows machine for VSCode

Open Windows Powershell

```
type $env:USERPROFILE\.ssh\id_rsa.pub | ssh [username]@192.168.1.xxx -p 2222 "cat >> .ssh/authorized_keys"
```

# add ssh config
```shell
sudo nano .ssh/config
```
add:
```
Host [name]
    HostName                192.168.1.xxx
    User                    [username]
    Port                    2222
```

# test it
```shell
ssh [name]
```
(should work without password)

# add startup rule to start ssh on laptop

- use `task scheduler` -> "Create Basic Task"
- name: "ssh"
- when: login
- script: `wsl`
- args: `-u root service ssh start`


# remove password login on laptop
```shell
sudo nano /etc/ssh/sshd_config
```
```
PasswordAuthentication no
```


# Mac

## Install bash
```
brew install bash
/opt/homebrew/bin/bash --version
sudo sh -c 'echo /opt/homebrew/bin/bash >> /etc/shells'
chsh -s /opt/homebrew/bin/bash
```
Restart terminal
```
echo $BASH_VERSION
```
Make bash default for root also
```
sudo chsh -s /usr/local/bin/bash
```
## add git completions
```
curl https://raw.githubusercontent.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash
```

