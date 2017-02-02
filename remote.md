# Remote working on Raspberry Pis

## Option 1: Remote with VNC

So long as your Raspberry Pis are networked, either via WiFi or a network switch, you can operate them remotely from any existing networked computer.

**V**irtual **N**etwork **C**omputing is a protocol that allows you to control one computer from another computer. The advantage of using VNC is that you gain access to the full desktop of the Raspberry Pi, meaning you can use graphical programs from the connected computer.

- First, you'll need to open a VNC server on your Raspberry Pi. Open a terminal and type in the following:

``` bash
vncserver
```

- When the VNC server starts, it will tell you which desktop you can use. Normally, this will be `:1` but it may be a different number:

![](images/vncserver.png)

- Now you can use another computer to control the Raspberry Pi. Depending on the OS of the client machine, there are a variety of apps you can use.

- You might find it useful to have the TightVNC server start every time the Raspberry Pi boots. To do this, you'll need to be `root` so open a terminal and type the following:

``` bash
sudo su
```

- Next, you need to navigate to the directory `/etc/init.d/` with the following command:

``` bash
cd /etc/init.d/
```

- Create a new file for the boot script:

``` bash
nano vncboot
```

- Then copy and paste the following script into the editor:

``` bash
#! /bin/sh
# /etc/init.d/vncboot

### BEGIN INIT INFO
# Provides: vncboot
# Required-Start: $remote_fs $syslog
# Required-Stop: $remote_fs $syslog
# Default-Start: 2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: Start VNC Server at boot time
# Description: Start VNC Server at boot time.
### END INIT INFO

USER=pi
HOME=/home/pi

export USER HOME

case "$1" in
 start)
  echo "Starting VNC Server"
  # Insert your preferred settings for a VNC session
  su - $USER -c "/usr/bin/vncserver :1 -geometry 1280x800 -depth 16 -pixelformat rgb565"
  ;;

 stop)
  echo "Stopping VNC Server"
  /usr/bin/vncserver -kill :1
  ;;

 *)
  echo "Usage: /etc/init.d/vncboot {start|stop}"
  exit 1
  ;;
esac

exit 0
```

- To exit nano, type `Ctrl+X`. Press `Y` to confirm the save and exit.

- Now you need to make the file executable:

``` bash
chmod 755 vncboot
```

- Then enable dependency-based boot sequencing:

``` bash
update-rc.d lightdm remove
update-rc.d vncboot defaults
```

- If enabling dependency-based boot sequencing was successful, you will see this:

``` bash
update-rc.d: using dependency based boot sequencing
```

- Now reboot your Raspberry Pi and you should find a VNC server already started.

- To connect to the Raspberry Pi from another computer, you can follow the instructions in one of the links below:

[On Windows](vnc-windows.md)  
[On OS X](vnc-osx.md)  
[On Chrome OS](vnc-chromeos.md)  
[On iOS](vnc-ios.md)  

- *Note* - Currently, software such as Minecraft, Picamera (preview) and omxplayer won't work over VNC. [RealVNC are working on an experimental server to rectify this](https://github.com/RealVNC/raspi-preview).

## Option 2 - Remote with SSH

If your students don't need access to a graphical user interface (GUI), then SSH is an easy way of connecting to, and using, Raspberry Pis.

### Linux-based operating systems

- If your students are using OS X or a Linux-based OS, then SSH is native to the operating system. Simply open a terminal and type:

``` bash
ssh pi@10.10.10.10
```

- Don't forget to replace 10.10.10.10 with the IP address of the Raspberry Pi.

- Then you can type in the password when prompted, usually `raspberry` unless you have changed it.

### Chrome OS and Chrome browser

- If your students are using Chrome OS or have access to the Chrome browser, then there's a Chrome app that allows access over SSH. You can find the Secure Shell App in the [Chrome Web Store](https://chrome.google.com/webstore/detail/secure-shell/pnhechapfaindjhompbnflcldabbghjo?hl=en).

![](images/chrome-ssh.png)

- Once installed, click on the app to open it:

![](images/chrome-ssh1.png)

- Now you can access the Raspberry Pi by typing in the IP address:

![](images/chrome-ssh2.png)

- Then type in the password:

![](images/chrome-ssh3.png)

### PuTTY (on Windows)

PuTTY is an app that provides SSH access on Windows.

- Download PuTTY from [this site](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

- Once installed, you can open PuTTY from the Start menu and type in the IP address:

![](images/ssh-win.png)

- If it's your first time connecting to this Raspberry Pi, you'll get a warning dialogue box, so click `Yes` to connect:

![](images/ssh-win2.png)

- Then you need to enter the username and password for the Raspberry Pi (usually `pi` and `raspberry`):

![](images/ssh-win3.png)
