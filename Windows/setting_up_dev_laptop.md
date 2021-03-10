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
[username]:x:1000:1000:,,,:/c/users/[username]:/bin/bash
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

# open port 2222 in windows
```
Right-click the Start button.
Click Search.
Type Windows Firewall.

Click Search. Type Windows Firewall.
Click Windows Firewall.
Click Advanced settings.

Click Windows Firewall. Click Advanced settings.
Click Inbound Rules in the left frame of the window.
Click New Rule… in the right frame of the window.

Click Inbound Rules. Click New Rule.
Click Port.
Click Next.

Click Port. Click Next.
Click either TCP or UDP.
Click Specific local ports.

Click either TCP or UDP. Click Specific local ports.
Type a port number. (In this case, we will open port 1707.)
Click Next.

Type a port number. Click Next.
Click Allow the connection.
Click Next.

Click Allow the connection. Click Next.
Click any network types you'd like to allow the connection over.
Click Next.

Click any network types. Click Next.
Type a name for the rule.
Click Finish.
```

# get local uri
```shell
ifconfig
```
look for `wifi0` (usually something like `192.168.1.xxx`)

# add keys to new server from other computer
```shell
ssh-copy-id -i ~/.ssh/id_rsa.pub [username]@192.168.1.xxx -p 2222
```
(you'll have to type password)

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
use `task scheduler`
command: `wsl`
args: `-u root service ssh start`
when: login

# remove password login on laptop
```shell
sudo nano /etc/ssh/sshd_config
```
```
PasswordAuthentication no
```
