# WSL Autostart
Support for starting the Linux services in Windows Subsystem for Linux (WSL) on Windows startup.

[README](README.md) | [中文文档](README_zh.md)

## Table of Contents

* [Installation](#installation)
* [Usage](#usage)

## Installation

* Clone to any directory using the git command: (e.g `C:\wsl-autostart`)
``` shell
git clone https://github.com/rescenic/wsl-autostart.git
```

* Add a startup item to the registry.<br/>
![run-regedit](doc/run-regedit.png)

* Add a string item under `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run` (e.g `WSLAutostart`) <br/>
![regedit-new-item](doc/regedit-new-item.png)

* Set the path to the script (e.g `C:\wsl-autostart\start.vbs`) <br/>
![regedit-set-path](doc/regedit-set-path.png)

## Usage

* Modify `/etc/sudoers` in the WSL to specify the service commands calling on startup without a password.
e.g:
``` sudoers
%sudo ALL=NOPASSWD: /etc/init.d/cron
%sudo ALL=NOPASSWD: /etc/init.d/ssh
#%sudo ALL=NOPASSWD: /etc/init.d/mysql
#%sudo ALL=NOPASSWD: /etc/init.d/apache2

%wheel ALL=NOPASSWD: /etc/init.d/cron
%wheel ALL=NOPASSWD: /etc/init.d/ssh
#%wheel ALL=NOPASSWD: /etc/init.d/mysql
#%wheel ALL=NOPASSWD: /etc/init.d/apache2

https://support.hostway.com/hc/en-us/articles/115001509750-How-To-Install-and-Configure-Sudo
```
* Modify `commands.txt` in the wsl-autostart directory to specify the service commands for your need.
e.g:
``` shell
/etc/init.d/cron
/etc/init.d/ssh
#/etc/init.d/mysql
#/etc/init.d/apache2
```

## Other methods
* Using `gpedit.msc`, it is possible to define a program that runs when the computer starts
  > Note that the configured program will run as the system user.
* Using `taskschd.msc`, it is possible to schedule a task after the startup of the computer.
  > You may configure which user will run the program, a delay before a run and a number of retries.
The same `taskschd.msc` program will show a specific log regarding the execution of the task

## Further reading: Install SSH on WSL
* https://superuser.com/questions/1111591/how-can-i-ssh-into-bash-on-ubuntu-on-windows-10
* https://gist.github.com/dentechy/de2be62b55cfd234681921d5a8b6be11
* https://gist.github.com/harleyday/76a103a1a0ca97c6f33706e4a8cc3307#file-wsl-ssh-server-md