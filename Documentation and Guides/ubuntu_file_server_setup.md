# Set up an Ubuntu File Server using the Samba protocol.

**NOTE:** *Unless stated otherwise, capitalized words in the following code blocks are user inputs and should be changed accordingly.*

## Setup 
1. Spin up a Ubuntu Server on Lightsail. Make sure it has enough SSD space.
2. Download the SSH key for the instance and make note of the public IP address for the server.
3. SSH in with:
    - `ssh -i PATH/TO/SSH/KEY ubuntu@IP.ADDRESS`

## Installation

1. First, ensure the server is up to date.
    - `sudo apt update -y && sudo apt upgrade -y`
    - Keep any AWS files and restart after updates are complete: `sudo shutdown -r now`
        - Restarting will disconnect you from the server. Reconnect with SSH as seen above after waiting a minute.
2. Install samba
    - `sudo apt install samba`
3. Setup a user for the backup share folder.
    - `sudo adduser USERNAME`
    - `sudo mkdir /home/USERNAME/share`

## Configuration
1. Open the samba configuration file
    - `sudo nano /etc/samba/smb.conf`
2. Add the following to the bottom.

```
[sambashare]
    comment = Samba on Ubuntu
    path = /home/USERNAME/share
    read only = no
    browsable = yes
```
Be sure to use the same absolute path as the share folder you created earlier.

Samba does not use the system password, so we must create a samba user and password with the following command. Use the same as we created earlier.
- `sudo smbpasswd -a USERNAME`


Next enable the new samba account.
- `sudo smbpasswd -e USERNAME`


## Firewall

Update  the firewall to allow connections on the samba ports:

- `sudo ufw allow samba`

Make note of the server's IP address (This is only necessary for a LAN server)
  - `ip a `

On Lightsail, use the **Networking** console to open the following ports:
- TCP: 139, 445
- UDP: 137, 138



## Mounting the Samba Fileserver as Net Drive 

### Windows

With a non-administrative cmd prompt:

    net use s: \\IP.ADDRESS\sambashare /user:USERNAME SAMBAPASSWORD /persistent:Yes

Check to see if the drive (S:) is visible in My Computer. If adding the net drive to a user account, this command may need to be run while logged into that account as well.
