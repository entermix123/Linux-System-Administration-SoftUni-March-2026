# Section 3 Introduction to Linux

Content

- [Section 3 Introduction to Linux](#section-3-introduction-to-linux)
  - [Install Linux on Oracle VirtualBox](#install-linux-on-oracle-virtualbox)
    - [Install Debian](#install-debian)
  - [Create and use Vurtual Machine Template](#create-and-use-vurtual-machine-template)
  - [Manage AlmaLinux VM](#manage-almalinux-vm)


<img src="pics/name.png" width="800" />
<br>
<br>

## Install Linux on Oracle VirtualBox

[⬆ Back to top](#top)

Donload and install Oracle VirtualBox - https://www.virtualbox.org/

Download Linux Debian install image - https://www.debian.org/

Create virtual machine on VirtualBox

### Install Debian

Create Virtual machine frame

<img src="pics/install-debian-1.png" width="800" />
<br>
<br>

<img src="pics/install-debian-2.png" width="800" />
<br>
<br>

<img src="pics/install-debian-3.png" width="800" />
<br>
<br>

Set the downloaded image

<img src="pics/install-debian-4.png" width="800" />
<br>
<br>

Start the machine

<img src="pics/install-debian-5.png" width="800" />
<br>
<br>

<img src="pics/install-debian-6.png" width="800" />
<br>
<br>

<img src="pics/install-debian-7.png" width="800" />
<br>
<br>

<img src="pics/install-debian-8.png" width="800" />
<br>
<br>

<img src="pics/install-debian-9.png" width="800" />
<br>
<br>

<img src="pics/install-debian-10.png" width="800" />
<br>
<br>

<img src="pics/install-debian-11.png" width="800" />
<br>
<br>

<img src="pics/install-debian-12.png" width="800" />
<br>
<br>

<img src="pics/install-debian-13.png" width="800" />
<br>
<br>

<img src="pics/install-debian-14.png" width="800" />
<br>
<br>

<img src="pics/install-debian-15.png" width="800" />
<br>
<br>

<img src="pics/install-debian-16.png" width="800" />
<br>
<br>

<img src="pics/install-debian-17.png" width="800" />
<br>
<br>

<img src="pics/install-debian-18.png" width="800" />
<br>
<br>

<img src="pics/install-debian-19.png" width="800" />
<br>
<br>

<img src="pics/install-debian-20.png" width="800" />
<br>
<br>

<img src="pics/install-debian-21.png" width="800" />
<br>
<br>

<img src="pics/install-debian-22.png" width="800" />
<br>
<br>

<img src="pics/install-debian-23.png" width="800" />
<br>
<br>

<img src="pics/install-debian-24.png" width="800" />
<br>
<br>

<img src="pics/install-debian-25.png" width="800" />
<br>
<br>

Wait until the machine is ready.

Login to the machine with regular user

<img src="pics/install-debian-26.png" width="800" />
<br>
<br>

Shut Down the machine

<img src="pics/install-debian-27.png" width="800" />
<br>
<br>

Set SSH connection with our local windows OS

<img src="pics/install-debian-28.png" width="800" />
<br>
<br>

<img src="pics/install-debian-29.png" width="800" />
<br>
<br>

Open SSH connection with the virtual machine

- Start the machine again

<img src="pics/install-debian-30.png" width="800" />
<br>
<br>

- Open SSH with the machine on Windows
  
    bash --> ssh -p 10001 user@localhost
    bash --> yes
    bash --> password

<img src="pics/install-debian-31.png" width="800" />
<br>
<br>

- Switch to root user and install sudo

  bash --> su -
  bash --> password

  bash --> apt update
  bash --> apt install sudo

- Add user 'user' to sudo list
  
  bash --> usermod -aG sudo user

- Exit the current session
  
  bash --> exit

- Login again with regular user and check if 'user' are in sudo list

  bash --> user   
  bash --> password   
  bash- -> id   

  result: 27(sudo)

- Shut down the machine from SSH

    bash --> sudo poweroff    
    bashh --> password
  
The VM is turning off

[⬆ Back to top](#top)

## Create and use Vurtual Machine Template

[⬆ Back to top](#top)


- Create VM machine Template
  
<img src="pics/vm-template-1.png" width="800" />
<br>
<br>

<img src="pics/vm-template-2.png" width="800" />
<br>
<br>

Wait untill the template is done

- Use VM template

<img src="pics/vm-template-use-1.png" width="800" />
<br>
<br>

<img src="pics/vm-template-use-2.png" width="800" />
<br>
<br>

- Clone VM machine

<img src="pics/vm-template-clone.png" width="800" />
<br>
<br>

[⬆ Back to top](#top)


## Manage AlmaLinux VM

[⬆ Back to top](#top)

Download Minimal AlmaLinux - https://almalinux.org/get-almalinux/

<h3>Install AlmaLinux with Oracle VirtualBox</h3>

<strong>Create bare VM</strong>

<img src="pics/alma-install-1.png" width="800" />
<br>
<br>

<img src="pics/alma-install-2.png" width="800" />
<br>
<br>

<img src="pics/alma-install-3.png" width="800" />
<br>
<br>

<strong>Configure AlmaLinux VM</strong>

<img src="pics/alma-install-5.png" width="800" />
<br>
<br>

<strong>Install ALmaLinux on VM</strong>

<img src="pics/alma-install-4.png" width="800" />
<br>
<br>

<img src="pics/alma-install-6.png" width="800" />
<br>
<br>

<img src="pics/alma-install-7.png" width="800" />
<br>
<br>

<img src="pics/alma-install-8.png" width="800" />
<br>
<br>

<img src="pics/alma-install-9.png" width="800" />
<br>
<br>

<img src="pics/alma-install-10.png" width="800" />
<br>
<br>

<img src="pics/alma-install-11.png" width="800" />
<br>
<br>

<img src="pics/alma-install-12.png" width="800" />
<br>
<br>

<img src="pics/alma-install-13.png" width="800" />
<br>
<br>

<img src="pics/alma-install-14.png" width="800" />
<br>
<br>

<img src="pics/alma-install-15.png" width="800" />
<br>
<br>

<img src="pics/alma-install-16.png" width="800" />
<br>
<br>

<img src="pics/alma-install-17.png" width="800" />
<br>
<br>

<img src="pics/alma-install-18.png" width="800" />
<br>
<br>

<img src="pics/alma-install-19.png" width="800" />
<br>
<br>

<img src="pics/alma-install-20.png" width="800" />
<br>
<br>

<strong>Export AlmaLinux VM Template</strong>

<img src="pics/alma-export-template.png" width="800" />
<br>
<br>

<img src="pics/alma-export-template-1.png" width="800" />
<br>
<br>

<strong>Import AlmaLinux VM Template</strong>

<img src="pics/alma-import-1.png" width="800" />
<br>
<br>

<img src="pics/alma-import-2.png" width="800" />
<br>
<br>

<strong>Clone AlmaLinux VM</strong>

<img src="pics/alma-clone.png" width="800" />
<br>
<br>

[⬆ Back to top](#top)