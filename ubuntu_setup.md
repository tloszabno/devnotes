# Ubuntu Setup - My own customizations


## Adjust Settings

* Go to Settings
  * Displays -> night light
    * set from 00:00 to 23:59
  * Appearance -> change dock size
    * set `24px`
  * Privacy
    * Screen lock
  	    * Show notification on Lock Screen -> off
  	    * Automatic Screen Lock -> off
    * Power
      * Power button action -> suspend
  * Keyboard shortcuts->
    * Home folder -> super + e
    * Terminal -> super + t
    * Mute -> super+crtl+m
    * Volume down -> super+ctrl+page down
    * Volume up -> super+ctrl+page up
* nvidia setting -> profiles
  * set `intel`
* Files -> Preferences-> Search & Preview-> Thumbnails
  * set `All files`
* Tweaks
	* Syspend when lid closed -> off
	* Desktop icons -> turn off
	* Activities Overview Hot Corner -> on
	* Windows Titlebars -> left



## Install Packages

```bash
sudo apt install -y python3-gpg keepassxc vlc git gitk vim vim-gtk guake gufw chrome-gnome-shell rar unrar p7zip-full p7zip-rar wine winetricks curl terminator fish mc qnapi ffmpeg python3-pip pipenv flameshot


pip install pep8
pip install --upgrade autopep8
```

## Install fonts

```bash
curl -L https://github.com/hbin/top-programming-fonts/raw/master/install.sh | bash
```

## Install autojump

```bash
git clone git://github.com/wting/autojump.git
cd autojump
./install.py
```

## Install your scripts

```bash
cd ~
git clone git@github.com:tloszabno/rivendell-scripts.git Scripts
ln -s ~/Scripts/config/tl.fish ~/.config/fish/conf.d/
ln -s ~/Scripts/config/autojump.fish ~/.config/fish/conf.d/
```


## Fix mouse issues

Microsoft mouse have scroll problem after wake up.

```bash
cd /lib/systemd/system-sleep/
sudo touch mouse.sh
sudo chmod +x mouse.sh
sudo vim mouse.sh
```
paste:

```bash
#!/bin/bash

#This is the fix for mircosoft mouse scrolling issue after wake from a suspension
if [[ $1 == post ]]; then
    modprobe -r usbhid
    modprobe usbhid
fi

```


## Configure Terminator

```
sudo update-alternatives --config x-terminal-emulator

curl -L https://get.oh-my.fish | fish

echo "alias mc 'mc --nosubshell'" >> /etc/fish/config.fish
```

### Settings
* Preferences
  * Profiles -> Scrolling
    * set `Infinite scrollback`

## Login to erebor (Raspberry pi) without password

```bash
ssh-keygen && cat ~/.ssh/id_rsa.pub | ssh pi@192.168.1.101 'cat >> .ssh/authorized_keys'
```

## Setup git

```bash
git config --global user.email "tloszabno@gmail.com"
git config --global user.name "Tomasz Los"
```

* add ssh key to github https://github.com/settings/keys

## Things to install manually

* Google Chrome
* Dropbox https://www.dropbox.com/pl/install-linux
* VS Code https://code.visualstudio.com/docs/?dv=linux64_deb
* https://velog.io/@spearkkk/Usage-jEnv-in-Fish + jenv install

## Other things to configure

* https://www.cyberciti.biz/faq/linux-unix-running-sudo-command-without-a-password/
* https://donjayamanne.github.io/pythonVSCodeDocs/docs/formatting/

## Review this pages for more adjustments

* https://www.omgubuntu.co.uk/2020/04/things-to-do-after-installing-ubuntu
* https://averagelinuxuser.com/after-installing-ubuntu-20-04/
