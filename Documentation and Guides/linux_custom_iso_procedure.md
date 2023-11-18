# Procedure to Create a New (or Alter) a Ubuntu ISO.
This procedure will show how to install Cubic, our ISO making software, and add packages to the ISO before finalizing. 

**WARNING:** The creation process of an ISO is a storage heavy procedure. If you are using a Virtual Machine, make sure you are using a large VDI. I recommend at least 50-60gbs as the ISO is built before being compressed and can take up a very large amount of space.

## Installation

First, ensure your Linux environment is fully updated and add the repositories necessary to install Cubic.
```
sudo apt update -y && sudo apt upgrade -y
sudo apt-add-repository universe
sudo apt-add-repository ppa:cubic-wizard/release
```

With the new repositories installed, update the repositoreies again and install cubic.
```
sudo apt update
sudo apt install cubic
```

## Building the ISO
Now you can launch Cubic through the terminal:
      
    cubic

![cubic_gui](https://static1.makeuseofimages.com/wordpress/wp-content/uploads/2022/11/source-and-custom.jpg?q=50&fit=crop&w=1500&dpr=1.5)

Using the latest LTS [Ubuntu Desktop ISO](https://ubuntu.com/download), create a folder for the ISO to be assembled and change the Disk Name to something related to the project or client at hand for easy referencing.

Click **Next**, and a specialized and containerized terminal (called a *chroot*) will launch. This is where we will be installed our packages.

First, update and upgrade the ISO.

```
sudo apt update -y && sudo apt upgrade -y
```

And next install your desired packages from `apt`, such as tmux, weechat, or tree. 


## Non-Apt Applications.
However, some applications will not be part of the standard Ubuntu repository. For those, we need a tricker solution. To demonstrate, we will use Google Chrome.

Using your normal Browser, nagivate to Chrome and download the latest .deb package from the website. In your Browser's Downloads tab, copy the Download Link for the package and paste it into a text edtior.

Inside the chroot terminal, use `wget` with that same download link to download the .deb package to your chroot environment.

```
wget "https://url/to/file.deb"
```

Once the package is installed, we can try to install it with apt. 

    sudo apt install ./downloaded_file.deb

If this doesn't work (chroot is a strange environment), then we can use the alternative method of 

    open downloaded_file.deb

Select "I" from following menu asking if you'd like to Install the package.

Do this repeatedly for each deb package you wish to install that is not included for Ubuntu package manager apt. 

If you'd like to remove any packages, feel free to do so with `apt purge`

    apt purge rhythmbox thunderbird firefox

Once, you are happy with the packages you want included in the ISO, click **Next**.

## Finalizing the ISO

![package selectpr](https://static1.makeuseofimages.com/wordpress/wp-content/uploads/2022/11/cubic-package-selection.jpg?q=50&fit=crop&w=1500&dpr=1.5)

Here you can decide which packages are included in normal installations of Ubuntu and which will be included with the Minimal Ubuntu installation. 

Click **Next** when you are done. Select the GZIP for the compression of the ISO and **Generate** the ISO.

After a few minutes, you should find a new ISO file saved to the folder you indicated earlier! Transfer to Avalon Lake fileserver aftewards for storage.
