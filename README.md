# MotivationStation2

Mp3Player Based on raspberry pi. If you close the contact on the GPIO17, it plays one random audio file from a USB stick

Clone into "/home/" directory

Requires

    python 3.5??? need to test without it
    mpg123
    RPI.GPIO
  
System mp3

A file named "system.mp3" in the same directory as the python script will play before playing a radom mp3 from the USB stick

All of the other the mp3's have to be on an usb stick in a directory named "mp3"

Mounting USB Stick

Create this directory 

    mkdir /mnt/usb 
open the file 

    sudo nano /etc/fstab 

and add the following line:

    /dev/sda1 /mnt/usb
    
Grant the script execute

    sudo chmod +x /home/MotivationStation2/mp3.sh
  
Start on boot

Create a file under /usr/lib/systemd/system and name it “playmp3.service”

    sudo nano /usr/lib/systemd/system/playmp3.service

Copy this inside the file you just created:

    [Unit]
    Description=PlayMP3
    After=multi-user.target

    [Service]
    Type=idle
    ExecStart=/usr/bin/python /home/MotivationStation2/play.py

    [Install]
    WantedBy=multi-user.target

To run the system on boot, do the following:

    sudo systemctl enable playmp3.service

Setup the USB SoundCard

    https://cdn-learn.adafruit.com/downloads/pdf/usb-audio-cards-with-a-raspberry-pi.pdf
    
    
Edit asound.conf to put the hardware sound card as primary. I'm using a CM 108 chipset soundcard

    sudo nano /etc/asound.conf and put the following in the file and save


    pcm.!default {
        type hw card 1
    }
    ctl.!default {
        type hw card 1
    }

Shutdown button on Pin 5 and Gnd 

Tutorial from https://pie.8bitjunkie.net/retropie-shutdown-and-startup-switch-the-easy-way#testing
    
    curl https://pie.8bitjunkie.net/shutdown/setup-shutdown.sh --output setup-shutdown.sh

    sudo chmod +x setup-shutdown.sh

    sudo ./setup-shutdown.sh
    
This seemed to work better than putting a shutdown script in rc.local manually. 
