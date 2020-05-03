# WSL Autostart
Support for starting the Linux services in Windows Subsystem for Linux (WSL) on Windows startup. <br/>
Additional features included:  Running `Ubuntu`, `Debian`, `Kali Linux` on Windows startup. See `control.bat`. <br/>
For example, I set SSH Port for `Ubuntu 401`, `Debian 403`, and `Kali Linux 404`.<br/>
![ssh-test](doc/ssh-test.png)

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
%sudo ALL=NOPASSWD: /etc/init.d/ssh
%sudo ALL=NOPASSWD: /usr/sbin/sshd
```

* Modify `commands.txt` in the wsl-autostart directory to specify the service commands for your need (Ubuntu, Debian, Kali Linux WSL).
e.g:
``` shell
/etc/init.d/ssh
/usr/sbin/sshd
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
* https://gist.github.com/dentechy/de2be62b55cfd234681921d5a8b6be11