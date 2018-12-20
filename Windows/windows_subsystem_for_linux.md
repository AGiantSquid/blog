## Use graphical programs
https://www.howtogeek.com/261575/how-to-run-graphical-linux-desktop-applications-from-windows-10s-bash-shell/

Download [VcXSrv](https://sourceforge.net/projects/vcxsrv/)

Get the Debian dependencies needed to run x11.
```bash
sudo apt-get install -y libcairo2-dev libgtk2.0-dev
```

## Setup dotfiles for Linux
```bash
alias config='/usr/bin/git --git-dir=$HOME/.myconfig/ --work-tree=$HOME'
echo ".myconfig" >> .gitignore
git clone --bare https://github.com/AGiantSquid/myconfig.git $HOME/.myconfig
```

## Install con emu

https://conemu.github.io/

- Navigate to settings > Start up > Tasks
- create a new task by hitting the plus button
- call it `{bash::debian}`
- Under the commands section, add `%windir%\system32\bash.exe ~ -cur_console:p`

