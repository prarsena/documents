How I set up my pi zero as a NAS (network attached storage) device 

Set up the SD Card
1.	Download the headless operating system (Rasbian lite) onto the MicroSD card. 
2.	Flash the OS image onto the MicroSD card using Etcher application.
3.	Unmount and mount (eject and reinsert) the drive to access it as an OS image. 
4.	Add an empty ssh file to the /boot/ drive: sudo touch ssh. 
5.	Add a wpa_supplicant.conf file to the /boot/ drive: sudo touch wpa_supplicant.conf
6.	Add the following information to the wpa_supplicant.conf file: sudo nano wpa_supplicant.conf

        country=US
        ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
        update_config=1

        network={
        ssid="WIFI_SSID"
        scan_ssid=1
        psk="WIFI_PASSWORD"
        key_mgmt=WPA-PSK
        }
 7. 
 
 Restart the Pi (unplug battery?). When the Pi starts up again, it should connect to your wifi within 30-45 seconds. 
 If you are re-installing the image and connecting to the os again, you have to modify your known-hosts file       
	
Connect to the RPI
1.	Ssh pi@raspberrypi.local
a.	User: pi
b.	Password: raspberry
c.	Change using passwd command once inside shell. 
2.	Update the OS: sudo apt-get update && sudo apt-get upgrade -y

Connect and mount a drive:
1.	Connect USB drive via the Micro USB slot. 
2.	Run sudo blkid to list the drives. Your USB might be listed under /dev/sda1
3.	Create a directory to hold volumes: sudo mkdir /mnt/volume
4.	Mount the drive to this directory: sudo mount /dev/sda1 /mnt/volume
// document set up automatic mounting. 

Set up samba
1.	Install samba: sudo apt-get install samba samba-common-bin
2.	Create a new share directory inside the USB drive:  sudo mkdir 1777 /mnt/volume/shared

Configure Samba to share this directory
1.	Edit the /etc/samba/smb.conf file to make this Shared folder visible to computers on the network: sudo nano /etc/samba/smb.conf:

          [PiShare]
          Comment = PI shared folder
          Path = /mnt/volume/shared
          Browseable = yes
          Writeable = Yes
          only guest = no
          create mask = 0777
          directory mask = 0777
          Public = yes
          Guest ok = yes 

You can set Public = No to require a registed user, and remove Guest ok = yes. 

Linux general add user:
1.	Sudo adduser tom
2.	Password: jerry

To remove a user
•	Userdel -r tom

Create Samba User
3.	Create a Samba user and password: sudo smbpasswd -a tom
a.	SMB Password: jerry
b.	System Password: jerry
2.	Restart Samba: sudo reboot

Add Samba password for pi user
•	Sudo smbpasswd -a pi 
•	SMB password: cake 

Find device in Mac: 
•	Finder > Go > Connect to Server: smb://raspberrypi.local 
•	Connect as Guest (if allowed) 
•	Connect as Registered User: pi/cake or tom/jerry  
•	Select your shared directory [PiShare]

Find device in Windows: 
•	Windows explorer for “This PC”
•	Click “Computer”
•	Click “Map Network Drives” 
•	Folder: \\raspberrypi\PiShare 

Shutdown:
	Sudo shutdown -h now
	
# Todo:
What is causing me problems?
- Connecting to a Plex server
- transferring files using scp to the NAS Share directory, or to a mounted directory in general. The permissions keep changing to root, even though I specify them as user owned in both /dev/sda1 and also /mnt/volume (assuming: sudo mount /dev/sda1/ /mnt/volume). That mounted drive is untouchable. 
- (aka) transferring files using scp to a mounted disk 
- Why when I reboot my OS, do I lose the ssh and wpa_supplicant.conf files i created? 

set up pihole
https://blog.cryptoaustralia.org.au/instructions-for-setting-up-pi-hole/

