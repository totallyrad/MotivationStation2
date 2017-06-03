# MotivationStation2

Mp3Player Based on raspberry pi. If you close the contact on the GPIO17, it plays a system sound "system.mp3" and then one random audio file from a USB stick

Clone into "/home/" directory

Requires

    python 3.5
    mpg123
    RPI.GPIO
  
System mp3

    A file named "system.mp3" in the same directory as the python script will play before playing a radon mp3 from the USB stick
    All of the other the mp3's have to be on an usb stick with a directory named "mp3"

Mounting USB Stick

    Now create this directory mkdir /mnt/usb 
    open the file /etc/fstab and add the following line:

    /dev/sda1 /mnt/usb
  
Start on boot

  Create a file under /usr/lib/systemd/system and name it “playmp3.service”

  Copy this inside the file you just created:

    [Unit]
    Description=PlayMP3
    After=multi-user.target

    [Service]
    Type=idle
    ExecStart=/usr/bin/python /home/play.py

    [Install]
    WantedBy=multi-user.target

  To run the system on boot, do the following:

  systemctl enable playmp3.service
