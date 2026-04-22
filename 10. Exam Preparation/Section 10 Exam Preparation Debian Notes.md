# Section 10 Exam Preparation

Content

- [Section 10 Exam Preparation](#section-10-exam-preparation)
  - [Theoretical Exam Simmulation](#theoretical-exam-simmulation)
  - [Practical Exam Simulation](#practical-exam-simulation)
    - [Exam task descrition](#exam-task-descrition)
      - [Disks and File Systems - 9 tasks, 13 pts](#disks-and-file-systems---9-tasks-13-pts)
      - [Directories and Files - 9 tasks, 16 pts](#directories-and-files---9-tasks-16-pts)
      - [Users and Permissions - 8 tasks, 12 pts](#users-and-permissions---8-tasks-12-pts)
      - [Software and Services - 7 tasks, 10 pts](#software-and-services---7-tasks-10-pts)
      - [Scripting and Schedules - 7 tasks, 11 pts](#scripting-and-schedules---7-tasks-11-pts)
    - [Approach - we will work over each task on VM1 and VM2 one by one. We will switch VMs for each different task no metter that we can continue with the next task on the current VM.](#approach---we-will-work-over-each-task-on-vm1-and-vm2-one-by-one-we-will-switch-vms-for-each-different-task-no-metter-that-we-can-continue-with-the-next-task-on-the-current-vm)
    - [VMs connection](#vms-connection)
    - [VM1](#vm1)
      - [Disks and File Systems - 9 tasks, 13 pts](#disks-and-file-systems---9-tasks-13-pts-1)
        - [(T101, 2 pts) VM1: Use the appropriate tool to create a new primary partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard disk drive with size of 800 MB and type set to Linux LVM](#t101-2-pts-vm1-use-the-appropriate-tool-to-create-a-new-primary-partition-using-the-mbr-partitioning-scheme-on-the-smaller-2-gb-and-empty-hard-disk-drive-with-size-of-800-mb-and-type-set-to-linux-lvm)
        - [(T102, 1 pts) VM1: Create a physical volume on the new partition, created earlier](#t102-1-pts-vm1-create-a-physical-volume-on-the-new-partition-created-earlier)
        - [(T103, 1 pts) VM1: Create a volume group named vg\_exam on the new physical volume](#t103-1-pts-vm1-create-a-volume-group-named-vg_exam-on-the-new-physical-volume)
        - [(T104, 1 pts) VM1: Create a logical volume named lv\_exam on the new volume group (use 100% of the available space in the volume group)](#t104-1-pts-vm1-create-a-logical-volume-named-lv_exam-on-the-new-volume-group-use-100-of-the-available-space-in-the-volume-group)
        - [(T105, 1 pts) VM1: Create an xfs file system on the lv\_exam logical volume](#t105-1-pts-vm1-create-an-xfs-file-system-on-the-lv_exam-logical-volume)
        - [(T106, 2 pts) VM1: Mount the new file system on the /data/xfs folder and add a record in the /etc/fstab file](#t106-2-pts-vm1-mount-the-new-file-system-on-the-dataxfs-folder-and-add-a-record-in-the-etcfstab-file)
      - [Directories and Files - 9 tasks, 16 pts](#directories-and-files---9-tasks-16-pts-1)
        - [(T201, 2 pts) VM1: Create series of directories under the path /data/projects with the following structure (refer to the image)](#t201-2-pts-vm1-create-series-of-directories-under-the-path-dataprojects-with-the-following-structure-refer-to-the-image)
        - [(T202, 1 pts) VM1: In each folder documents from the previous step create a text file named readme.txt that contains the text linux](#t202-1-pts-vm1-in-each-folder-documents-from-the-previous-step-create-a-text-file-named-readmetxt-that-contains-the-text-linux)
        - [(T203, 2 pts) VM1: In each folder source create a file named code.sh that contains just the signature for bash scripts and a single command - pwd](#t203-2-pts-vm1-in-each-folder-source-create-a-file-named-codesh-that-contains-just-the-signature-for-bash-scripts-and-a-single-command---pwd)
        - [(T204, 2 pts) VM1: Create a file named unique-animals.txt in the folder /data/animals that contains the sorted list in reverse order of the unique animals (just their names) found in the /important/animal-stories.txt file](#t204-2-pts-vm1-create-a-file-named-unique-animalstxt-in-the-folder-dataanimals-that-contains-the-sorted-list-in-reverse-order-of-the-unique-animals-just-their-names-found-in-the-importantanimal-storiestxt-file)
        - [(T205, 2 pts) VM1: Create a xz compressed archive named important-bak.tar.xz of the /important folder and its content and store it in the /data/archive folder](#t205-2-pts-vm1-create-a-xz-compressed-archive-named-important-baktarxz-of-the-important-folder-and-its-content-and-store-it-in-the-dataarchive-folder)
      - [Users and Permissions - 8 tasks, 12 pts](#users-and-permissions---8-tasks-12-pts-1)
        - [(T301, 2 pts) VM1: Create a user john with full name John Smith, with some password and auto-created home folder](#t301-2-pts-vm1-create-a-user-john-with-full-name-john-smith-with-some-password-and-auto-created-home-folder)
        - [(T302, 2 pts) VM1: Create a user jane with full name Jane Parker, with some password and auto-created home folder](#t302-2-pts-vm1-create-a-user-jane-with-full-name-jane-parker-with-some-password-and-auto-created-home-folder)
        - [(T303, 1 pts) VM1: Create a group named team](#t303-1-pts-vm1-create-a-group-named-team)
        - [(T304, 1 pts) VM1: Make both users, john and jane, part of the team group](#t304-1-pts-vm1-make-both-users-john-and-jane-part-of-the-team-group)
        - [(T305, 1 pts) VM1: Make user jane and group team owners of the /data/projects folder and all its sub-folders and files](#t305-1-pts-vm1-make-user-jane-and-group-team-owners-of-the-dataprojects-folder-and-all-its-sub-folders-and-files)
      - [Software and Services - 7 tasks, 10 pts](#software-and-services---7-tasks-10-pts-1)
        - [(T401, 1 pts) VM1: Visit https://repos.zahariev.pro/ and follow the instructions to register the repository on the machine](#t401-1-pts-vm1-visit-httpsreposzaharievpro-and-follow-the-instructions-to-register-the-repository-on-the-machine)
        - [(T403, 1 pts) VM1: Install the hello-lsa package from the repository registered in T401](#t403-1-pts-vm1-install-the-hello-lsa-package-from-the-repository-registered-in-t401)
        - [(T402, 2 pts) VM1: Create a file /data/repos/packages.txt with the list of all available packages in the repository registered in T401](#t402-2-pts-vm1-create-a-file-datarepospackagestxt-with-the-list-of-all-available-packages-in-the-repository-registered-in-t401)
      - [Scripting and Schedules - 7 tasks, 11 pts](#scripting-and-schedules---7-tasks-11-pts-1)
        - [(T501, 1 pts) VM1: Create a bash script file (should contain signature at least) named processes.sh in the /data/scripts folder](#t501-1-pts-vm1-create-a-bash-script-file-should-contain-signature-at-least-named-processessh-in-the-datascripts-folder)
        - [(T502, 1 pts) VM1: Change permissions of the /data/scripts/processes.sh file to executable for everyone](#t502-1-pts-vm1-change-permissions-of-the-datascriptsprocessessh-file-to-executable-for-everyone)
        - [(T503, 4 pts) VM1: When executed the processes.sh script should capture the date and time and the number of running processes and store (append) the results in the /tmp/processes.log file. For example, if the script is executed on 2026.04.09 at 10:15:53 and there are 82 processes, the row that would be stored in the file should be 2026-04-09 10-15-53 -\> 82](#t503-4-pts-vm1-when-executed-the-processessh-script-should-capture-the-date-and-time-and-the-number-of-running-processes-and-store-append-the-results-in-the-tmpprocesseslog-file-for-example-if-the-script-is-executed-on-20260409-at-101553-and-there-are-82-processes-the-row-that-would-be-stored-in-the-file-should-be-2026-04-09-10-15-53---82)
        - [(T504, 1 pts) VM1: Schedule the script for the exam user to execute every five minutes](#t504-1-pts-vm1-schedule-the-script-for-the-exam-user-to-execute-every-five-minutes)
    - [VM2](#vm2)
      - [Disks and File Systems - 9 tasks, 13 pts](#disks-and-file-systems---9-tasks-13-pts-2)
        - [(T107, 2 pts) VM2: Use the appropriate tool to create a new partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard drive with size of 650 MB and type set to Linux Filesystem](#t107-2-pts-vm2-use-the-appropriate-tool-to-create-a-new-partition-using-the-mbr-partitioning-scheme-on-the-smaller-2-gb-and-empty-hard-drive-with-size-of-650-mb-and-type-set-to-linux-filesystem)
        - [(T108, 1 pts) VM2: Create ext4 file system on the new partition](#t108-1-pts-vm2-create-ext4-file-system-on-the-new-partition)
        - [(T109, 2 pts) VM2: Mount the new file system on the /data/ext4 folder and add a record in the /etc/fstab file](#t109-2-pts-vm2-mount-the-new-file-system-on-the-dataext4-folder-and-add-a-record-in-the-etcfstab-file)
      - [Directories and Files - 9 tasks, 16 pts](#directories-and-files---9-tasks-16-pts-2)
        - [(T206, 2 pts) VM2: Create a text file exam-files.txt (and store it under /data/find folder) that contains the sorted (in ascending order) list of all the places (full path, including the name) where files with exam.lsa name are found](#t206-2-pts-vm2-create-a-text-file-exam-filestxt-and-store-it-under-datafind-folder-that-contains-the-sorted-in-ascending-order-list-of-all-the-places-full-path-including-the-name-where-files-with-examlsa-name-are-found)
        - [(T207, 1 pts) VM2: Create a new file based on the exam-files.txt with all words (in the file) exam changed to EXAM and store it as exam-files-upper.txt in the same folder (/data/find)](#t207-1-pts-vm2-create-a-new-file-based-on-the-exam-filestxt-with-all-words-in-the-file-exam-changed-to-exam-and-store-it-as-exam-files-uppertxt-in-the-same-folder-datafind)
        - [(T208, 2 pts) VM2: VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/lions.txt file which contains only lines that contain the lion text no matter the register (size of the letters) or position in a sentence](#t208-2-pts-vm2-vm2-create-a-copy-of-the-importantanimal-storiestxt-file-as-dataanimalslionstxt-file-which-contains-only-lines-that-contain-the-lion-text-no-matter-the-register-size-of-the-letters-or-position-in-a-sentence)
        - [(T209, 2 pts) VM2: VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/colors.txt file which contains only the unique in alphabetic order for all records about tigers](#t209-2-pts-vm2-vm2-create-a-copy-of-the-importantanimal-storiestxt-file-as-dataanimalscolorstxt-file-which-contains-only-the-unique-in-alphabetic-order-for-all-records-about-tigers)
      - [Users and Permissions - 8 tasks, 12 pts](#users-and-permissions---8-tasks-12-pts-2)
        - [(T306, 2 pts) VM2: Create a user jim with full name Jim Beam, with some password, auto-created home folder](#t306-2-pts-vm2-create-a-user-jim-with-full-name-jim-beam-with-some-password-auto-created-home-folder)
        - [(T307, 2 pts) VM2: Create a group named powerteam](#t307-2-pts-vm2-create-a-group-named-powerteam)
        - [(T308, 1 pts) VM2: Make the user jim part of the powerteam group](#t308-1-pts-vm2-make-the-user-jim-part-of-the-powerteam-group)
      - [Software and Services - 7 tasks, 10 pts](#software-and-services---7-tasks-10-pts-2)
        - [(T404, 2 pts) VM2: Install NGINX Web Server, start it, and enable it to run on boot](#t404-2-pts-vm2-install-nginx-web-server-start-it-and-enable-it-to-run-on-boot)
        - [(T405, 1 pts) VM2: Install the cowsay package and execute it with the following command cowsay 'Hello LSA(1)' \> ~/cowsay.txt](#t405-1-pts-vm2-install-the-cowsay-package-and-execute-it-with-the-following-command-cowsay-hello-lsa1--cowsaytxt)
        - [(T406, 1 pts) VM2: Download the appropriate package for your distribution:](#t406-1-pts-vm2-download-the-appropriate-package-for-your-distribution)
        - [(T407, 2 pts) VM2: Install the downloaded package (do not delete the downloaded file)](#t407-2-pts-vm2-install-the-downloaded-package-do-not-delete-the-downloaded-file)
      - [Scripting and Schedules - 7 tasks, 11 pts](#scripting-and-schedules---7-tasks-11-pts-2)
        - [(T505, 1 pts) VM2: Create a bash script file (should contain signature at least) named stars.sh in the /data/scripts folder](#t505-1-pts-vm2-create-a-bash-script-file-should-contain-signature-at-least-named-starssh-in-the-datascripts-folder)
        - [(T506, 1 pts) VM2: Change permissions of the /data/scripts/stars.sh file to executable for everyone](#t506-1-pts-vm2-change-permissions-of-the-datascriptsstarssh-file-to-executable-for-everyone)
        - [(T507, 2 pts) VM2: When executed the stars.sh script should accept one parameter (if not given, should return an error and exit) and print the symbol \* in a row as many times as specified by the parameter. For example, if the script is executed like this /data/scripts/stars.sh 5 then the result will be \*\*\*\*\*](#t507-2-pts-vm2-when-executed-the-starssh-script-should-accept-one-parameter-if-not-given-should-return-an-error-and-exit-and-print-the-symbol--in-a-row-as-many-times-as-specified-by-the-parameter-for-example-if-the-script-is-executed-like-this-datascriptsstarssh-5-then-the-result-will-be-)

## Theoretical Exam Simmulation

[⬆ Back to top](#top)

Pracice teoretical test - https://zahariev.rpo/q/sla

[⬆ Back to top](#top)

## Practical Exam Simulation

[⬆ Back to top](#top)

Start 1:51 from video



### Exam task descrition
#### Disks and File Systems - 9 tasks, 13 pts
• (T101, 2 pts) VM1: Use the appropriate tool to create a new primary partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard disk drive with size of 800 MB and type set to Linux LVM
• (T102, 1 pts) VM1: Create a physical volume on the new partition, created earlier
• (T103, 1 pts) VM1: Create a volume group named vg_exam on the new physical volume
• (T104, 1 pts) VM1: Create a logical volume named lv_exam on the new volume group (use 100% of the available space in the volume group)
• (T105, 1 pts) VM1: Create an xfs file system on the lv_exam logical volume
• (T106, 2 pts) VM1: Mount the new file system on the /data/xfs folder and add a record in the /etc/fstab file
• (T107, 2 pts) VM2: Use the appropriate tool to create a new partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard drive with size of 650 MB and type set to Linux Filesystem
• (T108, 1 pts) VM2: Create ext4 file system on the new partition
• (T109, 2 pts) VM2: Mount the new file system on the /data/ext4 folder and add a record in the /etc/fstab file

#### Directories and Files - 9 tasks, 16 pts
• (T201, 2 pts) VM1: Create series of directories under the path /data/projects with the following structure (refer to the image)
• (T202, 1 pts) VM1: In each folder documents from the previous step create a text file named readme.txt that contains the text linux
• (T203, 2 pts) VM1: In each folder source create a file named code.sh that contains just the signature for bash scripts and a single command - pwd

/data
└── projects
    ├── project1
    │ ├── documents
    │ └── source
    └── project2
      ├── documents
      └── source

• (T204, 2 pts) VM1: Create a file named unique-animals.txt in the folder /data/animals that contains the sorted list in reverse order of the unique animals (just their names) found in the /important/animal-stories.txt file
• (T205, 2 pts) VM1: Create a xz compressed archive named important-bak.tar.xz of the /important folder and its content and store it in the /data/archive folder
• (T206, 2 pts) VM2: Create a text file exam-files.txt (and store it under /data/find folder) that contains the sorted (in ascending order) list of all the places (full path, including the name) where files with exam.lsa name are found
• (T207, 1 pts) VM2: Create a new file based on the exam-files.txt with all words (in the file) exam changed to EXAM and store it as exam-files-upper.txt in the same folder (/data/find)
• (T208, 2 pts) VM2: VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/lions.txt file which contains only lines that contain the lion text no matter the register (size of the letters) or position in a sentence
• (T209, 2 pts) VM2: VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/colors.txt file which contains only the unique in alphabetic order for all records about tigers

#### Users and Permissions - 8 tasks, 12 pts
• (T301, 2 pts) VM1: Create a user john with full name John Smith, with some password and auto-created home
folder
• (T302, 2 pts) VM1: Create a user jane with full name Jane Parker, with some password and auto-created home
folder
• (T303, 1 pts) VM1: Create a group named team
• (T304, 1 pts) VM1: Make both users, john and jane, part of the team group
• (T305, 1 pts) VM1: Make user jane and group team owners of the /data/projects folder and all its sub-folders and files
• (T306, 2 pts) VM2: Create a user jim with full name Jim Beam, with some password, auto-created home folder
• (T307, 2 pts) VM2: Create a group named powerteam
• (T308, 1 pts) VM2: Make the user jim part of the powerteam group

#### Software and Services - 7 tasks, 10 pts
• (T401, 1 pts) VM1: Visit https://repos.zahariev.pro/ and follow the instructions to register the repository on the machine
• (T402, 2 pts) VM1: Create a file /data/repos/packages.txt with the list of all available packages in the repository registered in T401
• (T403, 1 pts) VM1: Install the hello-lsa package from the repository registered in T401
• (T404, 2 pts) VM2: Install NGINX Web Server, start it, and enable it to run on boot
• (T405, 1 pts) VM2: Install the cowsay package and execute it with the following command cowsay 'Hello LSA(1)' > ~/cowsay.txt
• (T406, 1 pts) VM2: Download the appropriate package for your distribution:
  o For Red Hat-based and openSUSE-based, download: https://zahariev.pro/linux/hello- lsa/releases/hello-lsa-1.0-1.el8.x86_64.rpm
  o For Debian-based, download: https://zahariev.pro/linux/hello-lsa/releases/hello-lsa-1.0_amd64.deb
• (T407, 2 pts) VM2: Install the downloaded package (do not delete the downloaded file)

#### Scripting and Schedules - 7 tasks, 11 pts
• (T501, 1 pts) VM1: Create a bash script file (should contain signature at least) named processes.sh in the
/data/scripts folder
• (T502, 1 pts) VM1: Change permissions of the /data/scripts/processes.sh file to executable for everyone
• (T503, 4 pts) VM1: When executed the processes.sh script should capture the date and time and the number of running processes and store (append) the results in the /tmp/processes.log file. For example, if the script is executed on 2026.04.09 at 10:15:53 and there are 82 processes, the row that would be stored in the file should be 2026-04-09 10-15-53 -> 82
• (T504, 1 pts) VM1: Schedule the script for the exam user to execute every five minutes
• (T505, 1 pts) VM2: Create a bash script file (should contain signature at least) named stars.sh in the /data/scripts folder
• (T506, 1 pts) VM2: Change permissions of the /data/scripts/stars.sh file to executable for everyone
• (T507, 2 pts) VM2: When executed the stars.sh script should accept one parameter (if not given, should return an error and exit) and print the symbol * in a row as many times as specified by the parameter.
For example, if the script is executed like this /data/scripts/stars.sh 5 then the result will be *****

### Approach - we will work over each task on VM1 and VM2 one by one. We will switch VMs for each different task no metter that we can continue with the next task on the current VM.

### VMs connection

Exam Preparation will be on Linux Debian. We can create 2 VMs in virtualbox and simulate the exam.

go to the address in the exam email - http://xx.xx.xx.xxx

Connect with SSH to the VMs in different consoles.

    console VM1 terminal --> ssh -p 10001 exam@192.168.1.22     # or user@localhost
    console VM2 terminal --> ssh -p 10002 exam@192.168.1.22

    
### VM1

#### Disks and File Systems - 9 tasks, 13 pts

##### (T101, 2 pts) VM1: Use the appropriate tool to create a new primary partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard disk drive with size of 800 MB and type set to Linux LVM

Show hard drives, we will use the one with 2GB space

    vm1 --> lsblk

Create disk on the sdb drive

    vm1 --> sudo fdisk /dev/sdb      # start manage disk sdb 2GB
    vm1 --> n                        # new partition   
    vm1 --> p                        # primary
    vm1 --> 1                        # 1st partition
    vm1 --> 2048                     # size - full disk size
    vm1 --> +800                     # +800MiB
    vm1 --> 1                        # type LVN and not Linux
    vm1 --> t                        # check types, LVV = 8E
    vm1 --> L                        # list options
    vm1 --> 8E                       # LVM 
    vm1 --> p                        # print and check for correct info
    vm1 --> w                        # save and quit  

Check disks again

    vm1 --> lsblk

##### (T102, 1 pts) VM1: Create a physical volume on the new partition, created earlier

Update the system

    vm1 --> sudo apt update

Install lvm2

    vm1 --> sudo apt install lvm2            # almalinux is using lvm by default
    vm1 --> y

Check disks - we will use sdb1

    vm1 --> lsblk

Create phisical volume

    vm1 --> sudo pvcreate /dev/sdb1

Cehck result

    vm1 --> sudo pvs


##### (T103, 1 pts) VM1: Create a volume group named vg_exam on the new physical volume

    vm1 --> sudo vgcreate vg_exam /dev/sdb1

Check result

    vm1 --> sudo vgs

##### (T104, 1 pts) VM1: Create a logical volume named lv_exam on the new volume group (use 100% of the available space in the volume group)

    vm1 --> sudo lvcreate -n lv_exam -l100%FREE vg_exam

Check result

    vm1 --> sudo lvs

##### (T105, 1 pts) VM1: Create an xfs file system on the lv_exam logical volume

Install xsf on Debian

    vm1 --> sudo apt install xfsprogs
    vm1 --> y

Create the file system
    
    vm1 --> sudo mkfs.xfs /dev/vg_exam/lv_exam


##### (T106, 2 pts) VM1: Mount the new file system on the /data/xfs folder and add a record in the /etc/fstab file

1. Create the record
2. test if the record point to the right file system

Check if the folder exist. In this case the fodler do not exist.

    vm1 --> ls -l /
  
Create the folder structure

    vm1 --> sudo mkdir -p /data/xfs

List the disks again to check the names

    vm1 --> lsblk

We can use the name - vg_exam-lv_exam or we can find the UUID of the disk

Find the UUID

    vm1 --> sudo blkid /dev/mapper/vg_exam-lv_exam

    # result: copy the UUID

Edit the config file fstab

    vm1 --> sudo vi /etc/fstab

Add UUID on the last line

```yaml
...

UUID='dsf9fsd8df-dfa8-af70-scf8-du8fsdfsd0d'    /data/xfs     xfs     defaults  0 0 
```
save and exit - :wq

Test the config

    vm1 --> sudo mount -av

Connect to VM2 to solve this task on it

#### Directories and Files - 9 tasks, 16 pts

##### (T201, 2 pts) VM1: Create series of directories under the path /data/projects with the following structure (refer to the image)

/data
└── projects
    ├── project1
    │ ├── documents
    │ └── source
    └── project2
      ├── documents
      └── source

Create the structure with one command

    vm1 --> sudo mkdir -pv /data/projects/project{1,2}/{documents,source}

    # -pv = -p - multilevel structure, v - verbose - give us the result on the console

Check the result with tree (if we have installed tree)

    vm1 --> tree /data/project


##### (T202, 1 pts) VM1: In each folder documents from the previous step create a text file named readme.txt that contains the text linux

Create the readem.xtx file and add text

    vm1 --> sudo vi /data/projects/project1/documents/readme.txt

```txt
linux
```
save and exit file - :wq

Copy the same file in the project 2 dir

    vm1 --> sudo cp /data/projects/project1/documents/readme.txt /data/projects/project2/documents/

Check the result:

    vm1 --> tree /data/projects/


##### (T203, 2 pts) VM1: In each folder source create a file named code.sh that contains just the signature for bash scripts and a single command - pwd

Create the script and set the signature and command in it

    vm1 --> sudo vi /data/projects/project1/source/code.sh

```sh
#!/bin/bash

pwd
```
save and exit file - :wq

Copy the file in the second project

    vm1 --> sudo cp /data/projects/project1/source/code.sh /data/projects/project2/source/

Check result

    vm1 --> tree /data/projects/


##### (T204, 2 pts) VM1: Create a file named unique-animals.txt in the folder /data/animals that contains the sorted list in reverse order of the unique animals (just their names) found in the /important/animal-stories.txt file

Create the required directory

    vm1 --> sudo mkdir -pv /data/animals

Check results

    vm1 --> tree /data/

Print the file on the console

    vm1 --> cat /important/animal-stories.txt

    # result:
    ...
    black-bats-are-slow-and-smell-bananas
    brown-snails-are-strong-and-smell-bananas
    ...

Filter and sort the required information - animals are the second objects

    vm1 --> cat /important/animal-stories.txt | cut -d '-' -f 2 | sort -r | uniq | sudo tee /data/animals/unique-animals.txt

    # separate every line by '-' (-d '-') and take second object  (-f 2) - the name of the animal
    # sort -r - sort in revese
    # uniq - take only unique objects
    # sudo tee /data/animals/unique-animals.txt - print result and save it in unique-animals.txt file

Check the file

    vm1 --> tree /data

Print the file

    vm1 --> cat /data/animals/unique-animals.txt

##### (T205, 2 pts) VM1: Create a xz compressed archive named important-bak.tar.xz of the /important folder and its content and store it in the /data/archive folder

Create the required directory

    vm1 --> sudo mkdir -p /data/archive

 Check the result

    vm1 --> tree /data   

Create the archive and save it in the required folder

    vm1 --> sudo tar -cJvf /data/achive/important-bak.tar.xz /important

Connect to VM2 to solve this task on it

#### Users and Permissions - 8 tasks, 12 pts

##### (T301, 2 pts) VM1: Create a user john with full name John Smith, with some password and auto-created home folder

    vm1 --> 

    vm1 --> 


##### (T302, 2 pts) VM1: Create a user jane with full name Jane Parker, with some password and auto-created home folder

Create user

    vm1 --> sudo useradd -m -c 'John Smith' john
    vm1 --> sudo useradd -m -c 'Jane Parker' jane

Set users passwords

    vm1 --> sudo passwd john
    vm1 --> somepass
    vm1 --> somepass

    vm1 --> sudo passwd jane
    vm1 --> somepass
    vm1 --> somepass
    
##### (T303, 1 pts) VM1: Create a group named team

Create group

    vm1 --> sudo groupadd team
    
##### (T304, 1 pts) VM1: Make both users, john and jane, part of the team group

    vm1 --> sudo usermod -aG team john
    vm1 --> sudo usermod -aG team jane

Check the results

    vm1 --> tail /etc/passwd
    vm1 --> tail /etc/group

##### (T305, 1 pts) VM1: Make user jane and group team owners of the /data/projects folder and all its sub-folders and files

Set the ownership - -Rv - recursive, verbose

    vm1 --> sudo chown -Rv jane:team /data/projects


Connect to VM2 to solve this task    


#### Software and Services - 7 tasks, 10 pts

##### (T401, 1 pts) VM1: Visit https://repos.zahariev.pro/ and follow the instructions to register the repository on the machine

Find the appropriate command on the address and use it

For APT (Debian 10.x/11.x/12.x/13.x, Ubuntu 20.x/21.x/22.x, etc.):

option 2.1 (amd64):

    vm1 --> echo "deb [arch=amd64] https://repos.zahariev.pro/apt stable main" | sudo tee /etc/apt/sources.list.d/zahariev-repo.list

##### (T403, 1 pts) VM1: Install the hello-lsa package from the repository registered in T401

Install the package with the given command on https://repos.zahariev.pro/

    vm1 --> sudo apt-get update --allow-insecure-repositories && sudo apt-get install hello-lsa

Check result:

    vm1 --> hello-sla

##### (T402, 2 pts) VM1: Create a file /data/repos/packages.txt with the list of all available packages in the repository registered in T401

Check if /data/repos exists and create it if not

    vm1 --> tree /data
    vm1 --> sudo mkdir -p /data/repos

List packages on the system

    vm1 --> sudo ls -al /var/lib/apt/lists

Save the filtered result in the required file

    vm1 --> grep ^Package: /var/lib/apt/lists/*zahariev*_Packages | sudo tee /data/repos/packages.txt

Check result

    vm1 --> tree /data
    vm1 --> cat /data/repos/packages.txt

Connect to VM2 and fisnish this task


#### Scripting and Schedules - 7 tasks, 11 pts

##### (T501, 1 pts) VM1: Create a bash script file (should contain signature at least) named processes.sh in the /data/scripts folder

Check if the folder exists and create it if not

    vm1 --> sudo mkdir -p /data/scripts

Check if the folder is created

    vm1 --> tree /data

Create the script

    vm1 --> sudo vi /data/scripts/processes.sh

```sh
#!/bin/bash
```
save the file and exit - :wq

Check the result:

    vm1 --> cat /data/scripts/processes.sh

##### (T502, 1 pts) VM1: Change permissions of the /data/scripts/processes.sh file to executable for everyone

Change the right for all - '-v' = verbose

    vm1 --> sudo chmod -v +x /data/scripts/processes.sh


##### (T503, 4 pts) VM1: When executed the processes.sh script should capture the date and time and the number of running processes and store (append) the results in the /tmp/processes.log file. For example, if the script is executed on 2026.04.09 at 10:15:53 and there are 82 processes, the row that would be stored in the file should be 2026-04-09 10-15-53 -> 82

Create the commands

The first command is for counting the processes - 'h' remove header from the result

    vm1 --> ps axh | wc -l

The second command is to present the current date is required format

    vm1 --> date '+%Y-%m-%d %H-%M-%S'

Edit the script file and combine the commands

    vm1 --> vi /data/processes.sh

```sh
#!/bin/bash

echo $(date '+Y%-%m-%d %H-%M-%S') '->' $(ps axh | wc -l) >> /tmp/processes.log
```
save the file and exit - :wq

Run the script and check the result

    vm1 --> /data/scripts/processes.sh
    vm1 --> cat /tmp/processes.log

Run the script and check the result again

    vm1 --> /data/scripts/processes.sh
    vm1 --> cat /tmp/processes.log


##### (T504, 1 pts) VM1: Schedule the script for the exam user to execute every five minutes

Create the cronjob executed for current user

    vm1 --> crontab -e

```yaml
*/5 * * * * /data/scripts/processes.sh
```
save and exit - :wq

Connect to VM2 to solve this task



### VM2

Connect to vm2 with ssh

    terminal --> ssh -p 10002 user@localhost

#### Disks and File Systems - 9 tasks, 13 pts

##### (T107, 2 pts) VM2: Use the appropriate tool to create a new partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard drive with size of 650 MB and type set to Linux Filesystem

List disks. The smaller disk is sdb1 and we will isntall on it.

    vm2 --> lsblk

Create partition

    vm2 --> sudo fdisk /dev/sdb       # set partition on disk
    vm2 --> n                         # new partition
    vm2 --> p                         # primary
    vm2 --> 1                         # first
    vm2 --> 2048                      # first sector size 
    vm2 --> +650M                     # 640MiB
    vm2 --> p                         # use default Linux partition type, print info
    vm2 --> w                         # save config

Check partitions. We should have sdb1 partition created.

    vm2 --> lsblk

##### (T108, 1 pts) VM2: Create ext4 file system on the new partition

Craete file system

    vm2 --> sudo mkfs.ext4 /dev/sdb1
    
##### (T109, 2 pts) VM2: Mount the new file system on the /data/ext4 folder and add a record in the /etc/fstab file

Check if directory /data/ext4 exits. In this case do not exist.

    vm2 --> ls -l /

Craete the required folder structure

    vm2 --> mkdir -p /data/ext4

Find the UUID of sdb1 and copy it

    vm2 --> sudo blkid /dev/sdb1

    # example result: UUID="adscca98-98cd-dfs7-cd8s-vssd7cd9vf"

Edit fstab and include the UUID

    vm2 --> sudo vi /etc/fstab

```yaml
...

UUID="adscca98-98cd-dfs7-cd8s-vssd7cd9vf"   /data/ext4    ext4    defaults    0 0
```
save the file and exit - :wq

Check the result

    vm2 --> sudo mount -av

Connect to VM1 to solve the next task

#### Directories and Files - 9 tasks, 16 pts

##### (T206, 2 pts) VM2: Create a text file exam-files.txt (and store it under /data/find folder) that contains the sorted (in ascending order) list of all the places (full path, including the name) where files with exam.lsa name are found

Create the required directory

    vm2 --> sudo mkdir -p /data/find

Check if the folder is created

    vm2 --> tree /data

Find all files 'exam.lsa' on the system and sort them ascending and save them in the file 

    cm2 --> sudo find / type f -name exam.lsa | sort | sudo tee /data/find/exam-files.txt

Check the result

    vm2 --> cat /data/find/exam-files.txt
    
##### (T207, 1 pts) VM2: Create a new file based on the exam-files.txt with all words (in the file) exam changed to EXAM and store it as exam-files-upper.txt in the same folder (/data/find)

Go true the file and replace the lowcase exam with uppercase EXAM in the file and save the result in required file.

    vm2 --> sed 's/exam/EXAM/g' /data/find/exam-files.txt | sudo tee /data/find/exam-files-upper.txt

Check if the file is created and rint it

    vm2 --> tree /data
    vm2 --> cat /data/find/exam-files-upper.txt
    
##### (T208, 2 pts) VM2: VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/lions.txt file which contains only lines that contain the lion text no matter the register (size of the letters) or position in a sentence

Check if the folder exists and if not create it

    vm2 --> tree /data/
    vm2 --> sudo mkdir -p /data/animals/

Check if the folder is created

    vm2 --> tree /data

Print the file with the text tp check what sorting we need to set

    vm2 --> cat /important/animal-stories.txt

Go true the file, sort the lines that contain 'lions' case unsesnsitive and save it in the required file
    
    vm2 --> cat /important/animal-stories.txt | grep -i lion | sudo tee /data/animals/lions.txt

Check if the file is created and print it

    vm2 --> tree /data
    vm2 --> cat /data/animals/lions.txt

##### (T209, 2 pts) VM2: VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/colors.txt file which contains only the unique in alphabetic order for all records about tigers

Check the information in the data file /important/animal-stories.txt

    vm2 --> cat /important/animal-stories.txt

    # result:
    brown-cougar-are-strong-and-eat-oranges
    shite-chameleons-are-weak-and-see-tomatoes
    ...

Sort the lines with tigers

    vm2 --> cat /important/animal-stories.txt | grep tigers | cut -d '-' -f 1 | sort | uniq | sudo tee /data/animals/colors.txt

Check if the file and its content

    vm2 --> tree /data
    vm2 --> cat /data/animals/colors.txt
    
Connect to VM1 to solve the next task

#### Users and Permissions - 8 tasks, 12 pts

##### (T306, 2 pts) VM2: Create a user jim with full name Jim Beam, with some password, auto-created home folder

Create user 

    vm2 --> sudo useradd -m -c 'Jim Beam' jim

Set jim password

    vm2 --> sudo passwd jim
    vm2 --> somepass
    vm2 --> somepass

##### (T307, 2 pts) VM2: Create a group named powerteam

Create 'powerteam' group with specific ID

    vm2 --> sudo groupadd -g 2100 powerteam


##### (T308, 1 pts) VM2: Make the user jim part of the powerteam group

Set jim to be member of powergroup group

    vm2 --> sudo usermod -aG powerteam jim

Check results

    vm2 --> tail /etc/passwd
    vm2 --> tail /etc/group

Connect to VM1 to solve next task



#### Software and Services - 7 tasks, 10 pts

##### (T404, 2 pts) VM2: Install NGINX Web Server, start it, and enable it to run on boot

Update the package manager

    vm2 --> sudo apt update

Install nginx

    vm2 --> sudo apt install nginx
    vm2 --> y

Check if nginx is running

    vm2 --> systemctl status nginx

##### (T405, 1 pts) VM2: Install the cowsay package and execute it with the following command cowsay 'Hello LSA(1)' > ~/cowsay.txt

Install cowsay package 

    vm2 --> sudo apt install cowsay

Execute command 'cowsay 'Hello LSA(1)' > ~/cowsay.txt'

    vm2 --> cowsay 'Hello LSA(1)' > ~/cowsay.txt

##### (T406, 1 pts) VM2: Download the appropriate package for your distribution:
  o For Red Hat-based and openSUSE-based, download: https://zahariev.pro/linux/hello- lsa/releases/hello-lsa-1.0-1.el8.x86_64.rpm
  o For Debian-based, download: https://zahariev.pro/linux/hello-lsa/releases/hello-lsa-1.0_amd64.deb

Download the appropriate package for debian distro

    vm2 --> wget https://zahariev.pro/linux/hello-lsa/releases/hello-lsa-1.0_amd64.deb

Check if it is downloaded successful

    vm2 --> ls

##### (T407, 2 pts) VM2: Install the downloaded package (do not delete the downloaded file)

Install the package

    vm2 --> sudo dpkg -i hello-lsa-1.0_amd64.deb

Test the package

    vm2 --> hello-sla

Connect to VM1 to solve next task

#### Scripting and Schedules - 7 tasks, 11 pts

##### (T505, 1 pts) VM2: Create a bash script file (should contain signature at least) named stars.sh in the /data/scripts folder

Check if /data/scripts exists and create it

    vm2 --> tree /data
    vm2 --> sudo mkdir -p /data/scripts

Check if the directory is created

    vm2 --> tree /data

Create the required script

    vm2 --> sudo vi /data/scripts/stars.sh

```sh
#!/bin/bash
```
save the file and exit - :wq

##### (T506, 1 pts) VM2: Change permissions of the /data/scripts/stars.sh file to executable for everyone

    vm2 --> sudo chmod -v +x /data/scripts/stars.sh
    
##### (T507, 2 pts) VM2: When executed the stars.sh script should accept one parameter (if not given, should return an error and exit) and print the symbol * in a row as many times as specified by the parameter. For example, if the script is executed like this /data/scripts/stars.sh 5 then the result will be *****

Create the commands

Create the first command for printing the stars

    vm2 --> for i in $(seq 1 5); do echo -n '*'; done; echo ''

Edit the script file and set the final script

    vm2 --> vi /data/scripts/stars.sh

```sh
#!/bin/bash

if [ $# -ne 1 ]; then
  echo 'Error';
  exit 1
fi

for i in $(seq 1 $1); do echo -n '*'; done ; echo ''
```
save the scrip and exit - :wq

Run the script with parameter

    vm2 --> /data/scripts/stars.sh 5

You made it ! Congrats !

[⬆ Back to top](#top)
