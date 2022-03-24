# PiLapse
chronicling my quest to set up a timelapse camera to watch my orchids bloom as a first foray into hardware

## Hardware
 * Raspberry Pi HQ Camera (12MP Sensor)
 * 6mm lens
 * Raspberry Pi Zero W
 * Zero Camera Cable 
 * Camera Mount Plate for Pi Zero 
 * 32GB microSD
 * mini tripod

## Set Up
After trying so many different combinations, here's what finally worked: 
  * load full size OS with SSH enabled to automatically connect to network on boot
  * follow [these instructions](https://www.instructables.com/How-to-Use-Ios-Devices-As-a-Monitor-of-Raspberry-P/) (loosely) - SSH into pi with `ssh pi@piname.local` and run `sudo apt-get install tightvncserver` and `tightvncserver` (set up password as requested)
  * enable Glamor in `sudo raspi-config` settings
  * download [VNC Viewer](https://www.realvnc.com/en/connect/download/vnc/macos/) and connect using the instructions above
  * run `libcamera-hello -t 0 --qt-preview` to get preview to focus

## Problems Along The Way
|problem | solution |
|*pi wouldn't connect to network via SSH after rebooting* | corrupted microSD, fixed when getting a new one |
|*couldn't focus camera in any shots* | remove C mount adapter ring from HQ camera base, start by turning focus adapter ring counter-clockwise 4-5 turns, adjust from there. be extremely patient. |
|*no way to view camera while focusing* | figured out how to use VNC viewer to view desktop - made focusing much easier |
|*preview window wouldn't open | * Enable Glamor in `sudo raspi-config` settings |

## Useful Commands

`scp pi@piname.local:/home/pi/*.jpg ./`
`tightvncserver`
`ssh-keygen -R *ip_address_or_hostname*` to remove ECSDA (?) key after reimaging with same name
`libcamera-hello -t 0 --qt-preview` 
`libcamera-still -o flowers.jpg`



