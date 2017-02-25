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
