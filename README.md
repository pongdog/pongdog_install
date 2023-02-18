# Pongdog installation instructions
#### This repository contains all the files required to install Pongdog. 

## How to install:
1. Clone this repository to your raspberry pi. 
2. Run the ```install.sh``` script as **sudo**. This will install the dependencies, as well as download and install docker. The rpi will reboot when completed. You may have to change the permission of the file: ```chmod a+rx install.sh```
3. Edit the configuration file ```config.toml``` to reflect the GPIO pins in which the button and LEDs are connected to the RPI. Use the GPIO-numbering, i.e. pin#37=26. Reference: https://www.raspberrypi.com/documentation/computers/images/GPIO-Pinout-Diagram-2.png .
Remember to set a unique table name for your table. The MQTT-settings should not need to be changed.
4. Edit the ```pongdogsound.service``` file so that the  ```WorkingDirectory``` is equal to the path to this folder (where you cloned the repo). Remember to also change the ```ExecStart``` path so that it points to the pongdog_sound binary located in this folder. If you cloned into the home folder, the path should be ```/home/pi/pongdog_install```
5. Start PongDog by running ```docker compose up -d``` in a terminal in the folder with the ```docker-compose.yml``` file. The service should now automatically start whenever the Pi reboots. 
6. Move the ```pongdogsound.service``` file to the systemmd-folder: ```cp pongdogsound.service /lib/systemd/system```. Enable the service ```sudo systemctl enable pongdogsound.service```. You can also start it immediately: ```sudo systemctl start pongdogsound.service```. 
