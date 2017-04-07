# Toggling-Lock
lock/unlock linux session using udev when new usb device is plugged/unplugged

* Unplug the device
* run on terminal:
`sudo udevadm monitor --property`
* plug the device.
* Identify the `ID_SERIAL` variable and get your value
* Edit the file /etc/udev/rules.d/51-android.rules and put this lines in end of file:
```
ACTION=="remove", ENV{ID_SERIAL}=="<PUT_SERIAL_HERE>", RUN+="/usr/local/bin/gnome-screensaver-lock"
ACTION=="add", ENV{ID_SERIAL}=="<PUT_SERIAL_HERE>", RUN+="/usr/local/bin/gnome-screensaver-unlock"
```

Create file `/usr/local/bin/gnome-screensaver-lock` with the follow content replacing `<username>` by your username:
```bash
#!/bin/sh
su <usrename> -c "DISPLAY=:0 XAUTHORITY=/home/<usrename>/.Xauthority /usr/bin/gnome-screensaver-command -l"
```
Create file `/usr/local/bin/gnome-screensaver-unlock` with the follow content replacing `<username>` by your username:
```bash
#!/bin/sh
su <usrename> -c "DISPLAY=:0 XAUTHORITY=/home/<usrename>/.Xauthority /usr/bin/gnome-screensaver-command -d"
```
Grant exec permissoin to files lock and unlock:
```bash
sudo chmod +x /usr/local/bin/gnome-screensaver-lock /usr/local/bin/gnome-screensaver-unlock
```
Now, test plugging and umplugging your device to your computer and... be happy!
