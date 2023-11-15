# Set up an Ubuntu File Server using the Samba protocol.

## Installation

1. First, ensure the server is up to date.
    - `sudo apt update -y && sudo apt upgrade -y`
2. Install samba
    - `sudo apt install samba`
3. Setup a share folder.
    - `mkdir ~/share`
    - `pwd` to make sure you know the absolute path to the folder. It will be used in the next step.

## Configuration
Using a text editor (`nano` is recommended), add the following to the end of the samba configuration file:

```
[sambashare]
    comment = Samba on Ubuntu
    path = /home/admin/share
    read only = no
    browsable = yes
```
Be sure to use the same absolute path as found earlier with `pwd`. The username may be different!

## Firewall
Update  the firewall to allow connections on the samba ports:

`sudo ufw allow samba`
