# install wsl
# install debain from store
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

# change linux home dir to /c/Users/[username]
```shell
sudo nano /etc/passwd
```
change
```
[username]:x:1000:1000:,,,:/home/[username]:/bin/bash
```
to
```
[username]:x:1000:1000:,,,:/c/Users/[username]:/bin/bash
```
Then restart wsl.

# change home dir permission to 700 (or ssh won't work)
```shell
cd
chmod 700 .
```

# install needed programs
```
sudo apt-get install openssh-server -y
sudo apt-get install git -y
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

# install dot files
# setup ssh to run on port 2222
Port 22 is taken by Windows
```shell
sudo nano /etc/ssh/sshd_config
```
change `#Port 22` to `Port 2222`

make sure:
```
PermitRootLogin no
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

# get local uri for dev machine wsl
```shell
ip a
```
look for `wifi0` if on wifi, or `eth0` if using a wired connection (usually something like `192.168.1.xxx`)

```shell
ip addr show dev eth0 | grep "inet " | awk '{ print $2 }' 
```

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
