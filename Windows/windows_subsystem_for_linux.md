## Use graphical programs
https://www.howtogeek.com/261575/how-to-run-graphical-linux-desktop-applications-from-windows-10s-bash-shell/

Download [xming](https://sourceforge.net/projects/xming/)

Get the Debian dependencies needed to run x11.
```
sudo apt-get install libcairo2-dev
apt-get install libgtk2.0-dev
```


alias config='/usr/bin/git --git-dir=$HOME/.myconfig/ --work-tree=$HOME'
echo ".myconfig" >> .gitignore
git clone --bare https://github.com/AGiantSquid/myconfig.git $HOME/.myconfig

## Install con emu

https://conemu.github.io/

- Navigate to settings > Start up > Tasks
- create a new task by hitting the plus button
- call it `{bash::debian}`
- Under the commands section, add `%windir%\system32\bash.exe ~ -cur_console:p`

