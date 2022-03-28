# PiLapse
chronicling my quest to set up a timelapse camera to watch my orchids bloom as a first foray into hardware! come along with me. 

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
  * download [VNC Viewer](https://www.realvnc.com/en/connect/download/vnc/macos/)
  * connect to pi with VNC Viewer with the pi's IP on the network (findable via your router admin page, i literally google 'router admin page' to find it) and the desktop number you get from `tightvncserver` (mine was 1) 
  * enable Glamor in Advanced section of `sudo raspi-config` settings
  * run `libcamera-hello -t 0 --qt-preview` to get preview to see the images while manually focusing the lens
  * run `libcamera-still -o flowers.jpg` to capture image
  * use `scp pi@piname.local:/home/pi/*.jpg ./` from a new terminal window to transfer over image files

## Problems Along The Way
| problem | solution |
|------- | ----------|
| *pi wouldn't connect to network via SSH after rebooting* | corrupted microSD, fixed when getting a new one |
| *wanted to focus pi camera* | tried an online hack of breaking the glue seal on a Pi Camera Module 2 and scratched the lens with tweezers and it was a very untenable strategy for focusing. ended up upgrading to the HQ camera which met the needs of the project much better. |
|*couldn't focus camera in any shots* | remove C mount adapter ring from HQ camera base, start by turning focus adapter ring counter-clockwise 4-5 turns, adjust from there. be extremely patient. |
|*no way to view camera while focusing* | figured out how to use VNC viewer to view desktop - made focusing much easier |
|*preview window wouldn't open* |  Enable Glamor in `sudo raspi-config` settings |

## Useful Commands

 * `tightvncserver` - run VNC server
 * `ssh-keygen -R *ip_address_or_hostname*` to remove ECSDA (?) key after reimaging with same name
 * `libcamera-hello -t 0 --qt-preview` - open preview indefinitely 
 * `libcamera-still -o flowers.jpg --qt-preview` capture still image with preview
 * `scp pi@piname.local:/home/pi/*.jpg ./` copy jpg files from command line
 * `libcamera-still -o test%04d.jpg -t 600000 --timelapse 10000 --vflip --hflip --immediate` - timelapse?

## Still Left To Do
 * figure out how to execute timelapse: picamera2? straight up libcamera + bash scripting? sleep overnight? 
 * figure out VNC viewer from iPhone for mobile explorations?

## Tutorials I Learned From 
 * [How to use Raspberry Pi Cameras with the New 'Bullseye' OS Update - LibCamera](https://www.youtube.com/watch?v=uw4jjvufU8Q)
 * [How to Use IOS Devices As a Monitor of Raspberry Pi](https://www.instructables.com/How-to-Use-Ios-Devices-As-a-Monitor-of-Raspberry-P/) 
 * [libcamera apps on Bullseye running on Pi 0 - 3](https://forums.raspberrypi.com/viewtopic.php?t=323547)
 * [Time Lapse Camera](https://dronebotworkshop.com/pi-10-timelapse/)
