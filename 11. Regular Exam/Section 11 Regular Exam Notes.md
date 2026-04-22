# Section 11 Regular Exam 19.04.2026

Content

- [Section 11 Regular Exam 19.04.2026](#section-11-regular-exam-19042026)
  - [Theoretical Exam Simmulation](#theoretical-exam-simmulation)
  - [Exam Description](#exam-description)
    - [Disks and File Systems - 9 tasks, 13 pts](#disks-and-file-systems---9-tasks-13-pts)
    - [Directories and Files - 9 tasks, 14 pts](#directories-and-files---9-tasks-14-pts)
    - [Users and Permissions - 8 tasks, 13 pts](#users-and-permissions---8-tasks-13-pts)
    - [Software and Services - 7 tasks, 9 pts](#software-and-services---7-tasks-9-pts)
    - [Scripting and Schedules - 7 tasks, 11 pts](#scripting-and-schedules---7-tasks-11-pts)
    - [Approach - we will work over each task on VM1 and VM2 one by one. We will switch VMs for each different task no metter that we can continue with the next task on the current VM.](#approach---we-will-work-over-each-task-on-vm1-and-vm2-one-by-one-we-will-switch-vms-for-each-different-task-no-metter-that-we-can-continue-with-the-next-task-on-the-current-vm)
    - [VMs connection](#vms-connection)
    - [VM1](#vm1)
      - [Disks and File Systems - 9 tasks, 13 pts](#disks-and-file-systems---9-tasks-13-pts-1)
        - [(T101, 2 pts) VM1: Use the appropriate tool to create a new primary partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard disk drive with size of 500 MB and type set to Linux LVM](#t101-2-pts-vm1-use-the-appropriate-tool-to-create-a-new-primary-partition-using-the-mbr-partitioning-scheme-on-the-smaller-2-gb-and-empty-hard-disk-drive-with-size-of-500-mb-and-type-set-to-linux-lvm)
        - [(T102, 1 pts) VM1: Create a physical volume on the new partition, created earlier](#t102-1-pts-vm1-create-a-physical-volume-on-the-new-partition-created-earlier)
        - [(T103, 1 pts) VM1: Create a volume group named vg\_exam on the new physical volume](#t103-1-pts-vm1-create-a-volume-group-named-vg_exam-on-the-new-physical-volume)
        - [(T104, 1 pts) VM1: Create a logical volume named lv\_exam on the new volume group (use 100% of the available space in the volume group)](#t104-1-pts-vm1-create-a-logical-volume-named-lv_exam-on-the-new-volume-group-use-100-of-the-available-space-in-the-volume-group)
        - [(T105, 1 pts) VM1: Create an xfs file system on the lv\_exam logical volume](#t105-1-pts-vm1-create-an-xfs-file-system-on-the-lv_exam-logical-volume)
        - [(T106, 2 pts) VM1: Mount the new file system on the /data/xfs folder and add a record in the /etc/fstab file](#t106-2-pts-vm1-mount-the-new-file-system-on-the-dataxfs-folder-and-add-a-record-in-the-etcfstab-file)
      - [Directories and Files - 9 tasks, 14 pts](#directories-and-files---9-tasks-14-pts-1)
        - [(T201, 2 pts) VM1: Create series of directories under the path /data/projects with the following structure (refer to the image)](#t201-2-pts-vm1-create-series-of-directories-under-the-path-dataprojects-with-the-following-structure-refer-to-the-image)
        - [(T202, 1 pts) VM1: In each folder documents from the previous step create an text file named readme.txt that contains the text kernel](#t202-1-pts-vm1-in-each-folder-documents-from-the-previous-step-create-an-text-file-named-readmetxt-that-contains-the-text-kernel)
        - [(T203, 1 pts) VM1: In each folder source create a file named code.sh that contains just the signature for bash scripts and a single command find](#t203-1-pts-vm1-in-each-folder-source-create-a-file-named-codesh-that-contains-just-the-signature-for-bash-scripts-and-a-single-command-find)
        - [(T204, 2 pts) VM1: Create a file named unique-animals.txt in the folder /data/animals that contains the sorted list in reverse order of the unique animals (just their names) found in the /important/animal-stories.txt file](#t204-2-pts-vm1-create-a-file-named-unique-animalstxt-in-the-folder-dataanimals-that-contains-the-sorted-list-in-reverse-order-of-the-unique-animals-just-their-names-found-in-the-importantanimal-storiestxt-file)
        - [(T205, 1 pts) VM1: Create a xz compressed archive named important-bak.tar.xz of the /important folder and its content and store it in the /data/archive folder](#t205-1-pts-vm1-create-a-xz-compressed-archive-named-important-baktarxz-of-the-important-folder-and-its-content-and-store-it-in-the-dataarchive-folder)
      - [Users and Permissions - 8 tasks, 13 pts](#users-and-permissions---8-tasks-13-pts-1)
        - [(T301, 2 pts) VM1: Create a user john with full name John Smith, with some password and auto-created home folder](#t301-2-pts-vm1-create-a-user-john-with-full-name-john-smith-with-some-password-and-auto-created-home-folder)
        - [(T302, 2 pts) VM1: Create a user tracy with full name Tracy Parker, with some password and auto-created home folder](#t302-2-pts-vm1-create-a-user-tracy-with-full-name-tracy-parker-with-some-password-and-auto-created-home-folder)
        - [(T303, 1 pts) VM1: Create a group named gurus](#t303-1-pts-vm1-create-a-group-named-gurus)
        - [(T304, 1 pts) VM1: Make both users, john and tracy, part of the gurus group](#t304-1-pts-vm1-make-both-users-john-and-tracy-part-of-the-gurus-group)
        - [(T305, 1 pts) VM1: Make user john and group gurus owners of the /data/projects folder and all its sub-folders and files](#t305-1-pts-vm1-make-user-john-and-group-gurus-owners-of-the-dataprojects-folder-and-all-its-sub-folders-and-files)
      - [Software and Services - 7 tasks, 9 pts](#software-and-services---7-tasks-9-pts-1)
        - [(T401, 1 pts) VM1: Visit https://repos.zahariev.pro/ and follow the instructions to register the repository on the machine](#t401-1-pts-vm1-visit-httpsreposzaharievpro-and-follow-the-instructions-to-register-the-repository-on-the-machine)
        - [(T403, 1 pts) VM1: Install the hello-lsa package from the repository registered in T401](#t403-1-pts-vm1-install-the-hello-lsa-package-from-the-repository-registered-in-t401)
        - [(T402, 2 pts) VM1: Create a file /data/repos/packages.txt with the list of all available packages in the repository registered in T401](#t402-2-pts-vm1-create-a-file-datarepospackagestxt-with-the-list-of-all-available-packages-in-the-repository-registered-in-t401)
      - [Scripting and Schedules - 7 tasks, 11 pts](#scripting-and-schedules---7-tasks-11-pts-1)
        - [(T501, 1 pts) VM1: Create a bash script file (should contain signature at least) named processes.sh in the /data/scripts folder](#t501-1-pts-vm1-create-a-bash-script-file-should-contain-signature-at-least-named-processessh-in-the-datascripts-folder)
        - [(T502, 1 pts) VM1: Change permissions of the /data/scripts/processes.sh file to executable for everyone](#t502-1-pts-vm1-change-permissions-of-the-datascriptsprocessessh-file-to-executable-for-everyone)
        - [(T503, 3 pts) VM1: When executed the processes.sh script should capture the date and time and the number of running processes and store (append) the results in the /tmp/processes.log file. For example, if the script is executed on 2026.04.19 at 10:15:53 and there are 82 processes, the row that would be stored in the file should be 2026.04.19 10.15.53 -\> 82](#t503-3-pts-vm1-when-executed-the-processessh-script-should-capture-the-date-and-time-and-the-number-of-running-processes-and-store-append-the-results-in-the-tmpprocesseslog-file-for-example-if-the-script-is-executed-on-20260419-at-101553-and-there-are-82-processes-the-row-that-would-be-stored-in-the-file-should-be-20260419-101553---82)
        - [(T504, 1 pts) VM1: Schedule the script for the exam user to execute every five minutes](#t504-1-pts-vm1-schedule-the-script-for-the-exam-user-to-execute-every-five-minutes)
    - [VM2](#vm2)
      - [Disks and File Systems - 9 tasks, 13 pts](#disks-and-file-systems---9-tasks-13-pts-2)
        - [(T107, 2 pts) VM2: Use the appropriate tool to create a new partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard drive with size of 850 MB and type set to Linux Filesystem](#t107-2-pts-vm2-use-the-appropriate-tool-to-create-a-new-partition-using-the-mbr-partitioning-scheme-on-the-smaller-2-gb-and-empty-hard-drive-with-size-of-850-mb-and-type-set-to-linux-filesystem)
        - [(T108, 1 pts) VM2: Create ext4 file system on the new partition](#t108-1-pts-vm2-create-ext4-file-system-on-the-new-partition)
        - [(T109, 2 pts) VM2: Mount the new file system on the /data/ext4 folder and add a record in the /etc/fstab file](#t109-2-pts-vm2-mount-the-new-file-system-on-the-dataext4-folder-and-add-a-record-in-the-etcfstab-file)
      - [Directories and Files - 9 tasks, 14 pts](#directories-and-files---9-tasks-14-pts-2)
        - [(T206, 2 pts) VM2: Create a text file exam-files.txt (and store it under /data/find folder) that contains the sorted (in ascending order) list of all the places (full path, including the name) where files with exam.lsa name are found](#t206-2-pts-vm2-create-a-text-file-exam-filestxt-and-store-it-under-datafind-folder-that-contains-the-sorted-in-ascending-order-list-of-all-the-places-full-path-including-the-name-where-files-with-examlsa-name-are-found)
        - [(T207, 1 pts) VM2: Create a new file based on the exam-files.txt with all words (in the file) exam changed to EXAM and store it as exam-files-upper.txt in the same folder (/data/find)](#t207-1-pts-vm2-create-a-new-file-based-on-the-exam-filestxt-with-all-words-in-the-file-exam-changed-to-exam-and-store-it-as-exam-files-uppertxt-in-the-same-folder-datafind)
        - [(T208, 2 pts) VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/lions.txt file which contains only lines that contain the lion text no matter the register (size of the letters) or position in a sentence](#t208-2-pts-vm2-create-a-copy-of-the-importantanimal-storiestxt-file-as-dataanimalslionstxt-file-which-contains-only-lines-that-contain-the-lion-text-no-matter-the-register-size-of-the-letters-or-position-in-a-sentence)
        - [(T209, 2 pts) VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/colors.txt file which contains only the unique colors in alphabetic order for all records about dogs](#t209-2-pts-vm2-create-a-copy-of-the-importantanimal-storiestxt-file-as-dataanimalscolorstxt-file-which-contains-only-the-unique-colors-in-alphabetic-order-for-all-records-about-dogs)
      - [Users and Permissions - 8 tasks, 13 pts](#users-and-permissions---8-tasks-13-pts-2)
        - [(T306, 2 pts) VM2: Create a user jim with full name Jim Beam, with some password and auto-created home folder](#t306-2-pts-vm2-create-a-user-jim-with-full-name-jim-beam-with-some-password-and-auto-created-home-folder)
        - [(T307, 2 pts) VM2: Create a group named powerteam with group ID set to 2300](#t307-2-pts-vm2-create-a-group-named-powerteam-with-group-id-set-to-2300)
        - [(T308, 2 pts) VM2: Make the user jim part of the powerteam group](#t308-2-pts-vm2-make-the-user-jim-part-of-the-powerteam-group)
      - [Software and Services - 7 tasks, 9 pts](#software-and-services---7-tasks-9-pts-2)
        - [(T404, 1 pts) VM2: Install NGINX Web Server, start it, and enable it to run on boot](#t404-1-pts-vm2-install-nginx-web-server-start-it-and-enable-it-to-run-on-boot)
        - [(T405, 1 pts) VM2: Install the cowsay package and execute it with the following command cowsay 'Hello LSA(3)' \> ~/cowsay.txt](#t405-1-pts-vm2-install-the-cowsay-package-and-execute-it-with-the-following-command-cowsay-hello-lsa3--cowsaytxt)
        - [(T406, 1 pts) VM2: Download the appropriate package for your distribution in the home folder of the exam user:](#t406-1-pts-vm2-download-the-appropriate-package-for-your-distribution-in-the-home-folder-of-the-exam-user)
        - [(T407, 2 pts) VM2: Install the downloaded package (do not delete the downloaded file)](#t407-2-pts-vm2-install-the-downloaded-package-do-not-delete-the-downloaded-file)
      - [Scripting and Schedules - 7 tasks, 11 pts](#scripting-and-schedules---7-tasks-11-pts-2)
        - [(T505, 1 pts) VM2: Create a bash script file (should contain signature at least) named symbols.sh in the /data/scripts folder](#t505-1-pts-vm2-create-a-bash-script-file-should-contain-signature-at-least-named-symbolssh-in-the-datascripts-folder)
        - [(T506, 1 pts) VM2: Change permissions of the /data/scripts/symbols.sh file to executable for everyone](#t506-1-pts-vm2-change-permissions-of-the-datascriptssymbolssh-file-to-executable-for-everyone)
        - [(T507, 3 pts) VM2: When executed the symbols.sh script should accept one parameter (if not given, should return an error and exit) and print the symbol \* in a row as many times as specified by the parameter. For example, if the script is executed like this /data/scripts/symbols.sh 4 then the result will be \*\*\*\*](#t507-3-pts-vm2-when-executed-the-symbolssh-script-should-accept-one-parameter-if-not-given-should-return-an-error-and-exit-and-print-the-symbol--in-a-row-as-many-times-as-specified-by-the-parameter-for-example-if-the-script-is-executed-like-this-datascriptssymbolssh-4-then-the-result-will-be-)

## Theoretical Exam Simmulation

[⬆ Back to top](#top)

Pracice teoretical test - https://zahariev.rpo/q/sla

[⬆ Back to top](#top)

## Exam Description

[⬆ Back to top](#top)

### Disks and File Systems - 9 tasks, 13 pts

    (T101, 2 pts) VM1: Use the appropriate tool to create a new primary partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard disk drive with size of 500 MB and type set to Linux LVM
    (T102, 1 pts) VM1: Create a physical volume on the new partition, created earlier
    (T103, 1 pts) VM1: Create a volume group named vg_exam on the new physical volume
    (T104, 1 pts) VM1: Create a logical volume named lv_exam on the new volume group (use 100% of the available space in the volume group)
    (T105, 1 pts) VM1: Create an xfs file system on the lv_exam logical volume
    (T106, 2 pts) VM1: Mount the new file system on the /data/xfs folder and add a record in the /etc/fstab file
    (T107, 2 pts) VM2: Use the appropriate tool to create a new partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard drive with size of 850 MB and type set to Linux Filesystem
    (T108, 1 pts) VM2: Create ext4 file system on the new partition
    (T109, 2 pts) VM2: Mount the new file system on the /data/ext4 folder and add a record in the /etc/fstab file

### Directories and Files - 9 tasks, 14 pts

    (T201, 2 pts) VM1: Create series of directories under the path /data/projects with the following structure (refer to the image)

/data
└── projects
    ├── project1
    │ ├── documents
    │ └── source
    └── project2
      ├── documents
      └── source

    (T202, 1 pts) VM1: In each folder documents from the previous step create an text file named readme.txt that contains the text kernel
    (T203, 1 pts) VM1: In each folder source create a file named code.sh that contains just the signature for bash scripts and a single command find
    (T204, 2 pts) VM1: Create a file named unique-animals.txt in the folder /data/animals that contains the sorted list in reverse order of the unique animals (just their names) found in the /important/animal-stories.txt file
    (T205, 1 pts) VM1: Create a xz compressed archive named important-bak.tar.xz of the /important folder and its content and store it in the /data/archive folder
    (T206, 2 pts) VM2: Create a text file exam-files.txt (and store it under /data/find folder) that contains the sorted (in ascending order) list of all the places (full path, including the name) where files with exam.lsa name are found
    (T207, 1 pts) VM2: Create a new file based on the exam-files.txt with all words (in the file) exam changed to EXAM and store it as exam-files-upper.txt in the same folder (/data/find)
    (T208, 2 pts) VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/lions.txt file which contains only lines that contain the lion text no matter the register (size of the letters) or position in a sentence
    (T209, 2 pts) VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/colors.txt file which contains only the unique colors in alphabetic order for all records about dogs

### Users and Permissions - 8 tasks, 13 pts

    (T301, 2 pts) VM1: Create a user john with full name John Smith, with some password and auto-created home folder
    (T302, 2 pts) VM1: Create a user tracy with full name Tracy Parker, with some password and auto-created home folder
    (T303, 1 pts) VM1: Create a group named gurus
    (T304, 1 pts) VM1: Make both users, john and tracy, part of the gurus group
    (T305, 1 pts) VM1: Make user john and group gurus owners of the /data/projects folder and all its sub-folders and files
    (T306, 2 pts) VM2: Create a user jim with full name Jim Beam, with some password and auto-created home folder
    (T307, 2 pts) VM2: Create a group named powerteam with group ID set to 2300
    (T308, 2 pts) VM2: Make the user jim part of the powerteam group


### Software and Services - 7 tasks, 9 pts

    (T401, 1 pts) VM1: Visit https://repos.zahariev.pro/ and follow the instructions to register the repository on the machine
    (T402, 2 pts) VM1: Create a file /data/repos/packages.txt with the list of all available packages in the repository registered in T401
    (T403, 1 pts) VM1: Install the hello-lsa package from the repository registered in T401
    (T404, 1 pts) VM2: Install NGINX Web Server, start it, and enable it to run on boot
    (T405, 1 pts) VM2: Install the cowsay package and execute it with the following command cowsay 'Hello LSA(3)' > ~/cowsay.txt
    (T406, 1 pts) VM2: Download the appropriate package for your distribution in the home folder of the exam user:
    o For Red Hat-based and openSUSE-based distributions, download: https://zahariev.pro/linux/hello-lsa/releases/hello-lsa-1.0-1.el8.x86_64.rpm
    o For Debian-based distributions, download: https://zahariev.pro/linux/hello-lsa/releases/hello-lsa-1.0_amd64.deb
    (T407, 2 pts) VM2: Install the downloaded package (do not delete the downloaded file)


### Scripting and Schedules - 7 tasks, 11 pts

    (T501, 1 pts) VM1: Create a bash script file (should contain signature at least) named processes.sh in the /data/scripts folder
    (T502, 1 pts) VM1: Change permissions of the /data/scripts/processes.sh file to executable for everyone
    (T503, 3 pts) VM1: When executed the processes.sh script should capture the date and time and the number of running processes and store (append) the results in the /tmp/processes.log file.
    For example, if the script is executed on 2026.04.19 at 10:15:53 and there are 82 processes, the row that would be stored in the file should be 2026.04.19 10.15.53 -> 82
    (T504, 1 pts) VM1: Schedule the script for the exam user to execute every five minutes
    (T505, 1 pts) VM2: Create a bash script file (should contain signature at least) named symbols.sh in the /data/scripts folder
    (T506, 1 pts) VM2: Change permissions of the /data/scripts/symbols.sh file to executable for everyone
    (T507, 3 pts) VM2: When executed the symbols.sh script should accept one parameter (if not given, should return an error and exit) and print the symbol * in a row as many times as specified by the parameter.
    For example, if the script is executed like this /data/scripts/symbols.sh 4 then the result will be ****



### Approach - we will work over each task on VM1 and VM2 one by one. We will switch VMs for each different task no metter that we can continue with the next task on the current VM.

### VMs connection

Exam Preparation will be on AlmaLinux. We can create 2 VMs in virtualbox and simulate the exam.

go to the address in the exam email - http://xx.xx.xx.xxx

Connect with SSH to the VMs in different consoles.

    console VM1 terminal --> ssh -p 10001 exam@45.66.47.116
    console VM2 terminal --> ssh -p 10002 exam@45.66.47.116

    
### VM1

Connect to vm1 with ssh

    terminal --> ssh -p 10001 user@localhost

Udate dnf package manager

    vm1 --> sudo dnf update

Install epel-release, tar, tree, bash autocomplete

    vm1 --> sudo dnf install epel-release tar tree bash-completion 

#### Disks and File Systems - 9 tasks, 13 pts

##### (T101, 2 pts) VM1: Use the appropriate tool to create a new primary partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard disk drive with size of 500 MB and type set to Linux LVM

Show hard drives, we will use the one with 2GB space

    vm1 --> lsblk

    # result:
    NAME               MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
    sda                  8:0    0    2G  0 disk                 # target disk
    sdb                  8:16   0   32G  0 disk
    ├─sdb1               8:17   0    1M  0 part
    ├─sdb2               8:18   0    1G  0 part /boot
    └─sdb3               8:19   0   31G  0 part
      ├─almalinux-root 253:0    0 27.8G  0 lvm  /
      └─almalinux-swap 253:1    0  3.2G  0 lvm  [SWAP]
    sr0                 11:0    1 1024M  0 rom

Create disk on the sda drive

    vm1 --> sudo fdisk /dev/sda      # start manage disk sdb 2GB
    vm1 --> n                        # new partition   
    vm1 --> p                        # primary
    vm1 --> 1                        # 1st partition
    vm1 --> 2048                     # size - full disk size
    vm1 --> +800                     # +800MiB
    vm1 --> t                        # List types, LVV = 8E
    vm1 --> L                        # list options
    vm1 --> 8E                       # LVM 
    vm1 --> p                        # print and check for correct info
    vm1 --> w                        # save and quit  

    # result:
    The partition table has been altered.
    Calling ioctl() to re-read partition table.
    Syncing disks.

Check disks again

    vm1 --> lsblk

    # result:
    NAME               MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
    sda                  8:0    0    2G  0 disk
    └─sda1               8:1    0  500M  0 part
    sdb                  8:16   0   32G  0 disk
    ├─sdb1               8:17   0    1M  0 part
    ├─sdb2               8:18   0    1G  0 part /boot
    └─sdb3               8:19   0   31G  0 part
      ├─almalinux-root 253:0    0 27.8G  0 lvm  /
      └─almalinux-swap 253:1    0  3.2G  0 lvm  [SWAP]
    sr0                 11:0    1 1024M  0 rom

##### (T102, 1 pts) VM1: Create a physical volume on the new partition, created earlier

    vm1 -->  sudo pvcreate /dev/sda1

    # result:   Physical volume "/dev/sda1" successfully created.

Check result

    vm1 --> sudo pvs

    # result: 
      PV         VG        Fmt  Attr PSize   PFree
      /dev/sda1            lvm2 ---  500.00m 500.00m
      /dev/sdb3  almalinux lvm2 a--  <31.00g      0

##### (T103, 1 pts) VM1: Create a volume group named vg_exam on the new physical volume

    vm1 --> sudo vgcreate vg_exam /dev/sda1

    # result:     Volume group "vg_exam" successfully created

Check result

    vm1 --> sudo vgs

    # result:
      VG        #PV #LV #SN Attr   VSize   VFree
      almalinux   1   2   0 wz--n- <31.00g      0
      vg_exam     1   0   0 wz--n- 496.00m 496.00m

##### (T104, 1 pts) VM1: Create a logical volume named lv_exam on the new volume group (use 100% of the available space in the volume group)

    vm1 --> sudo lvcreate -n lv_exam -l100%FREE vg_exam

    # result:  Logical volume "lv_exam" created.

Check result

    vm1 --> sudo lvs

    # result:
      LV      VG        Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
      root    almalinux -wi-ao----  27.79g
      swap    almalinux -wi-ao----   3.20g
      lv_exam vg_exam   -wi-a----- 496.00m

##### (T105, 1 pts) VM1: Create an xfs file system on the lv_exam logical volume

Create the file system
    
    vm1 --> sudo mkfs.xfs /dev/vg_exam/lv_exam

    # result:
    meta-data=/dev/vg_exam/lv_exam   isize=512    agcount=4, agsize=31744 blks
            =                       sectsz=4096  attr=2, projid32bit=1
            =                       crc=1        finobt=1, sparse=1, rmapbt=1
            =                       reflink=1    bigtime=1 inobtcount=1 nrext64=1
            =                       exchange=0
    data     =                       bsize=4096   blocks=126976, imaxpct=25
            =                       sunit=0      swidth=0 blks
    naming   =version 2              bsize=4096   ascii-ci=0, ftype=1, parent=0
    log      =internal log           bsize=4096   blocks=16384, version=2
            =                       sectsz=4096  sunit=1 blks, lazy-count=1
    realtime =none                   extsz=4096   blocks=0, rtextents=0
    Discarding blocks...Done.

##### (T106, 2 pts) VM1: Mount the new file system on the /data/xfs folder and add a record in the /etc/fstab file

1. Create the record
2. test if the record point to the right file system

Check if the folder exist. In this case the fodler do not exist.

    vm1 --> ls -l /
  
Create the folder structure

    vm1 --> sudo mkdir -p /data/xfs

    vm1 --> tree /data

    # result:
    /data
        └── xfs

List the disks again to check the names

    vm1 --> lsblk

    # result:
    NAME                MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
    sda                   8:0    0   32G  0 disk
    ├─sda1                8:1    0    1M  0 part
    ├─sda2                8:2    0    1G  0 part /boot
    └─sda3                8:3    0   31G  0 part
        ├─almalinux-root  253:0    0   29G  0 lvm  /
        └─almalinux-swap  253:1    0    2G  0 lvm  [SWAP]
    sdb                   8:16   0    2G  0 disk
    └─sdb1                8:17   0  800M  0 part
        └─vg_exam-lv_exam 253:2    0  796M  0 lvm
    sr0                  11:0    1 1024M  0 rom

We can use the name - vg_exam-lv_exam or we can find the UUID of the disk

Find the UUID

    vm1 --> sudo blkid /dev/mapper/vg_exam-lv_exam

    # result: copy the  UUID="0e73fcb2-8b23-4691-ba4c-c9f7b2a99511"

Edit the config file fstab

    vm1 --> sudo vi /etc/fstab

Add UUID on the last line

```yaml
...

UUID="0e73fcb2-8b23-4691-ba4c-c9f7b2a99511"    /data/xfs          xfs     defaults        0 0 
```
save and exit - :wq

Test the config

    vm1 --> sudo mount -av

    # result:
    /                        : ignored
    /boot                    : already mounted
    none                     : ignored
    mount: /data/xfs does not contain SELinux labels.
          You just mounted a file system that supports labels which does not
          contain labels, onto an SELinux box. It is likely that confined
          applications will generate AVC messages and not be allowed access to
          this file system.  For more details see restorecon(8) and mount(8).
    mount: (hint) your fstab has been modified, but systemd still uses
          the old version; use 'systemctl daemon-reload' to reload.
    /data/xfs                : successfully mounted

Connect to VM2 and finish the task


#### Directories and Files - 9 tasks, 14 pts

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

    # result:
    mkdir: created directory '/data/projects'
    mkdir: created directory '/data/projects/project1'
    mkdir: created directory '/data/projects/project1/documents'
    mkdir: created directory '/data/projects/project1/source'
    mkdir: created directory '/data/projects/project2'
    mkdir: created directory '/data/projects/project2/documents'
    mkdir: created directory '/data/projects/project2/source'


##### (T202, 1 pts) VM1: In each folder documents from the previous step create an text file named readme.txt that contains the text kernel

Create the readem.xtx file and add text

    vm1 --> sudo vi /data/projects/project1/documents/readme.txt

```txt
kernel
```
save and exit file - :wq

Print the file

    vm1 --> cat /data/projects/project1/documents/readme.txt

Copy the same file in the project 2 dir

    vm1 --> sudo cp /data/projects/project1/documents/readme.txt /data/projects/project2/documents/

Check the result:

    vm1 --> tree /data/projects/

    # result:
    /data/projects/
    ├── project1
    │   ├── documents
    │   │   └── readme.txt
    │   └── source
    └── project2
        ├── documents
        │   └── readme.txt
        └── source


##### (T203, 1 pts) VM1: In each folder source create a file named code.sh that contains just the signature for bash scripts and a single command find

Create the script and set the signature and command in it

    vm1 --> sudo vi /data/projects/project1/source/code.sh

```sh
#!/bin/bash

find
```
save and exit file - :wq

Copy the file in the second project

    vm1 --> sudo cp /data/projects/project1/source/code.sh /data/projects/project2/source/

Check result

    vm1 --> tree /data/projects/

    # result:
    /data/projects/
    ├── project1
    │   ├── documents
    │   │   └── readme.txt
    │   └── source
    │       └── code.sh
    └── project2
        ├── documents
        │   └── readme.txt
        └── source
            └── code.sh


##### (T204, 2 pts) VM1: Create a file named unique-animals.txt in the folder /data/animals that contains the sorted list in reverse order of the unique animals (just their names) found in the /important/animal-stories.txt file

Create the required directory

    vm1 --> sudo mkdir -pv /data/animals

    # result: mkdir: created directory '/data/animals'

Check results

    vm1 --> tree /data

    # result:
    /data
    ├── animals                         # created
    ├── projects
    │   ├── project1
    │   │   ├── documents
    │   │   │   └── readme.txt
    │   │   └── source
    │   │       └── code.sh
    │   └── project2
    │       ├── documents
    │       │   └── readme.txt
    │       └── source
    │           └── code.sh
    └── xfs

Print the file on the console

    vm1 --> cat /important/animal-stories.txt

    # result:
    ...
    yellow+snails+are+strong+and+smell+tomatoes
    yellow+foxes+are+clever+and+like+tomatoes
    pink+pandas+are+fast+and+smell+kiwis
    yellow+chameleons+are+good+and+smell+oranges
    yellow+snakes+are+blind+and+see+bananas
    brown+cats+are+blind+and+smell+tomatoes
    ...

Filter and sort the required information - animals are the second objects

    vm1 --> cat /important/animal-stories.txt | cut -d '+' -f 2 | sort -r | uniq | sudo tee /data/animals/unique-animals.txt

    # separate every line by '+' (-d '+') and take second object  (-f 2) - the name of the animal
    # sort -r - sort in revese
    # uniq - take only unique objects
    # sudo tee /data/animals/unique-animals.txt - print result and save it in unique-animals.txt file

Check the file

    vm1 --> tree /data

    # result:
    /data
    ├── animals
    │   └── unique-animals.txt        # created
    ├── projects
    │   ├── project1
    │   │   ├── documents
    │   │   │   └── readme.txt
    │   │   └── source
    │   │       └── code.sh
    │   └── project2
    │       ├── documents
    │       │   └── readme.txt
    │       └── source
    │           └── code.sh
    └── xfs

Print the file

    vm1 --> cat /data/animals/unique-animals.txt

    # result:
    wolves
    whales
    tigers
    snakes
    snails
    rabbits
    ...

##### (T205, 1 pts) VM1: Create a xz compressed archive named important-bak.tar.xz of the /important folder and its content and store it in the /data/archive folder

Create the required directory

    vm1 --> sudo mkdir -p /data/archive

 Check the result

    vm1 --> tree /data   

    # result:
    /data
    ├── animals
    │   └── unique-animals.txt
    ├── archive                   # created folder
    ...

Create the archive and save it in the required folder

    vm1 --> sudo tar -cJvf /data/archive/important-bak.tar.xz /important

    # result:
    tar: Removing leading `/' from member names
    /important/
    /important/animal-stories.txt

 Check the result

    vm1 --> tree /data   

    # result:
    /data
    ├── animals
    │   └── unique-animals.txt
    ├── archive
    │   └── important-bak.tar.xz        # created archive
    ...

Connect to VM2 to solve this task

#### Users and Permissions - 8 tasks, 13 pts

##### (T301, 2 pts) VM1: Create a user john with full name John Smith, with some password and auto-created home folder

##### (T302, 2 pts) VM1: Create a user tracy with full name Tracy Parker, with some password and auto-created home folder

Create users

    vm1 --> sudo useradd -m -c 'John Smith' john
    vm1 --> sudo useradd -m -c 'Tracy Parker' tracy

Set users passwords

    vm1 --> sudo passwd john
    vm1 --> somepass
    vm1 --> somepass

    vm1 --> sudo passwd tracy
    vm1 --> somepass
    vm1 --> somepass

##### (T303, 1 pts) VM1: Create a group named gurus

Create group

    vm1 --> sudo groupadd gurus

##### (T304, 1 pts) VM1: Make both users, john and tracy, part of the gurus group

    vm1 --> sudo usermod -aG gurus john
    vm1 --> sudo usermod -aG gurus tracy

Check the results

    vm1 --> tail /etc/passwd

    # result:
    ...
    john:x:1001:1001:John Smith:/home/john:/bin/bash
    tracy:x:1002:1002:Tracy Parker:/home/tracy:/bin/bash
    ...

    vm1 --> tail /etc/group

    # result:
    ...
    gurus:x:1003:john,tracy

##### (T305, 1 pts) VM1: Make user john and group gurus owners of the /data/projects folder and all its sub-folders and files

Set the ownership - -Rv - recursive, verbose

    vm1 --> sudo chown -Rv john:gurus /data/projects

    # result:
    changed ownership of '/data/projects/project1/documents/readme.txt' from root:root to john:gurus
    changed ownership of '/data/projects/project1/documents' from root:root to john:gurus
    changed ownership of '/data/projects/project1/source/code.sh' from root:root to john:gurus
    changed ownership of '/data/projects/project1/source' from root:root to john:gurus
    changed ownership of '/data/projects/project1' from root:root to john:gurus
    changed ownership of '/data/projects/project2/documents/readme.txt' from root:root to john:gurus
    changed ownership of '/data/projects/project2/documents' from root:root to john:gurus
    changed ownership of '/data/projects/project2/source/code.sh' from root:root to john:gurus
    changed ownership of '/data/projects/project2/source' from root:root to john:gurus
    changed ownership of '/data/projects/project2' from root:root to john:gurus
    changed ownership of '/data/projects' from root:root to john:gurus

Connect to VM2 and solve this task


#### Software and Services - 7 tasks, 9 pts

##### (T401, 1 pts) VM1: Visit https://repos.zahariev.pro/ and follow the instructions to register the repository on the machine

Find the appropriate command on the address and use it

First install this 

    vm1 --> sudo dnf install 'dnf-command(config-manager)'

For DNF/YUM (AlmaLinux OS 8.x/9.x/10.x, Rocky Linux 8.x/9.x/10.x, etc.):

option 2

    vm1 --> sudo dnf config-manager --add-repo https://repos.zahariev.pro/dnf

##### (T403, 1 pts) VM1: Install the hello-lsa package from the repository registered in T401

Install the package with the given command on https://repos.zahariev.pro/

    vm1 --> sudo dnf install --nogpgcheck hello-lsa

Check result:

    vm1 --> hello-lsa

    # result:
     _   _      _ _         _     ____    _
    | | | | ___| | | ___   | |   / ___|  / \
    | |_| |/ _ \ | |/ _ \  | |   \___ \ / _ \
    |  _  |  __/ | | (_) | | |___ ___) / ___ \
    |_| |_|\___|_|_|\___/  |_____|____/_/   \_\



##### (T402, 2 pts) VM1: Create a file /data/repos/packages.txt with the list of all available packages in the repository registered in T401

Check if /data/repos exists and create it if not

    vm1 --> tree /data
    vm1 --> sudo mkdir -p /data/repos

List packages on the system

    vm1 --> sudo dnf repolist

    # result:
    repo id                                repo name
    appstream                              AlmaLinux 10 - AppStream
    baseos                                 AlmaLinux 10 - BaseOS
    crb                                    AlmaLinux 10 - CRB
    epel                                   Extra Packages for Enterprise Linux 10 - x86_64
    extras                                 AlmaLinux 10 - Extras
    repos.zahariev.pro_dnf                 created by dnf config-manager from https://repos.zahariev.pro/dnf        # target repo, we use repo id

Save the filtered result in the required file

    vm1 --> sudo dnf repoquery --repoid=repos.zahariev.pro_dnf --queryformat="%{name}" | sudo tee /data/repos/packages.txt

    # result:
    Last metadata expiration check: 0:07:07 ago on Sat Apr 18 21:31:00 2026.
    hello-lsa

Check result

    vm1 --> tree /data
    vm1 --> cat /data/repos/packages.txt

    # result: 
    hello-lsa


Connect to VM2 and solve this task


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

    # result: mode of '/data/scripts/processes.sh' changed from 0644 (rw-r--r--) to 0755 (rwxr-xr-x)

##### (T503, 3 pts) VM1: When executed the processes.sh script should capture the date and time and the number of running processes and store (append) the results in the /tmp/processes.log file. For example, if the script is executed on 2026.04.19 at 10:15:53 and there are 82 processes, the row that would be stored in the file should be 2026.04.19 10.15.53 -> 82

Create the commands

The first command is for counting the processes - 'h' remove header from the result

    vm1 --> ps axh | wc -l

The second command is to present the current date is required format

    vm1 --> date '+%Y-%m-%d %H-%M-%S'

Edit the script file and combine the commands

    vm1 --> sudo vi /data/scripts/processes.sh

```sh
#!/bin/bash

echo $(date '+%Y-%m-%d %H-%M-%S') '->' $(ps axh | wc -l) >> /tmp/processes.log
```
save the file and exit - :wq

Run the script and check the result

    vm1 --> /data/scripts/processes.sh
    vm1 --> cat /tmp/processes.log

    # re sult: 2026-04-18 21-43-26 -> 122

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

Connect to VM2 and solve this task


### VM2

Connect to vm2 with ssh

    terminal --> ssh -p 10002 user@localhost

Udate dnf package manager

    vm2 --> sudo dnf update

Install epel-release, tar, tree, bash autocomplete

    vm2 --> sudo dnf install epel-release tar tree bash-completion

#### Disks and File Systems - 9 tasks, 13 pts

##### (T107, 2 pts) VM2: Use the appropriate tool to create a new partition using the MBR partitioning scheme on the smaller (2 GB) and empty hard drive with size of 850 MB and type set to Linux Filesystem

List disks. The smaller disk is sdb1 and we will isntall on it.

    vm2 --> lsblk

    # result:
    NAME               MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
    sda                  8:0    0   32G  0 disk
    ├─sda1               8:1    0    1M  0 part
    ├─sda2               8:2    0    1G  0 part /boot
    └─sda3               8:3    0   31G  0 part
      ├─almalinux-root 253:0    0 27.8G  0 lvm  /
      └─almalinux-swap 253:1    0  3.2G  0 lvm  [SWAP]
    sdb                  8:16   0    2G  0 disk
    sr0                 11:0    1 1024M  0 rom

Create partition

    vm2 --> sudo fdisk /dev/sdb       # set partition on disk
    vm2 --> n                         # new partition
    vm2 --> p                         # primary
    vm2 --> 1                         # first
    vm2 --> 2048                      # first sector size 
    vm2 --> +850M                     # 850MiB
    vm2 --> p                         # use default Linux partition type, print info
    vm2 --> w                         # save config

    # result:
    The partition table has been altered.
    Calling ioctl() to re-read partition table.
    Syncing disks.

Check partitions. We should have sdb1 partition created.

    vm2 --> lsblk

    # result:
    NAME               MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
    sda                  8:0    0   32G  0 disk
    ├─sda1               8:1    0    1M  0 part
    ├─sda2               8:2    0    1G  0 part /boot
    └─sda3               8:3    0   31G  0 part
      ├─almalinux-root 253:0    0 27.8G  0 lvm  /
      └─almalinux-swap 253:1    0  3.2G  0 lvm  [SWAP]
    sdb                  8:16   0    2G  0 disk
    └─sdb1               8:17   0  850M  0 part           # craeted
    sr0                 11:0    1 1024M  0 rom

##### (T108, 1 pts) VM2: Create ext4 file system on the new partition

Craete file system

    vm2 --> sudo mkfs.ext4 /dev/sdb1

    # result:
    mke2fs 1.47.1 (20-May-2024)
    Discarding device blocks: done
    Creating filesystem with 217600 4k blocks and 54432 inodes
    Filesystem UUID: 286db4d5-3296-4afd-9385-c053db708834
    Superblock backups stored on blocks:
            32768, 98304, 163840

    Allocating group tables: done
    Writing inode tables: done
    Creating journal (4096 blocks): done
    Writing superblocks and filesystem accounting information: done

##### (T109, 2 pts) VM2: Mount the new file system on the /data/ext4 folder and add a record in the /etc/fstab file

Check if directory /data/ext4 exits. In this case do not exist.

    vm2 --> ls -l /

Craete the required folder structure

    vm2 --> sudo mkdir -p /data/ext4

Check the created file

    vm2 --> tree /data

    # result:
    /data
    └── ext4

Find the UUID of sdb1 and copy it

    vm2 --> sudo blkid /dev/sdb1

    # example result: UUID="286db4d5-3296-4afd-9385-c053db708834"

Edit fstab and include the UUID

    vm2 --> sudo vi /etc/fstab

```yaml
...

UUID="286db4d5-3296-4afd-9385-c053db708834"   /data/ext4          ext4    defaults        0 0
```
save the file and exit - :wq

Mount the file system

    vm2 --> sudo mount -av

    # result:
    /                        : ignored
    /boot                    : already mounted
    none                     : ignored
    mount: /data/ext4 does not contain SELinux labels.
          You just mounted a file system that supports labels which does not
          contain labels, onto an SELinux box. It is likely that confined
          applications will generate AVC messages and not be allowed access to
          this file system.  For more details see restorecon(8) and mount(8).
    mount: (hint) your fstab has been modified, but systemd still uses
          the old version; use 'systemctl daemon-reload' to reload.
    /data/ext4               : successfully mounted

Connect to VM1 to solve the next task

#### Directories and Files - 9 tasks, 14 pts

##### (T206, 2 pts) VM2: Create a text file exam-files.txt (and store it under /data/find folder) that contains the sorted (in ascending order) list of all the places (full path, including the name) where files with exam.lsa name are found

Create the required directory

    vm2 --> sudo mkdir -p /data/find

Check if the folder is created

    vm2 --> tree /data

    # result:
    /data
    ├── ext4
    │   └── lost+found  [error opening dir]
    └── find

Find all files 'exam.lsa' on the system and sort them ascending and save them in the file 

    cm2 --> sudo find / -type f -name exam.lsa | sort | sudo tee /data/find/exam-files.txt

    # result:
    find: ‘type’: No such file or directory
    find: ‘f’: No such file or directory
    /etc/exam.lsa
    /exam.lsa
    /tmp/exam.lsa
    /usr/share/exam.lsa

Check the result

    vm2 --> tree /data

    # result:
    /data
    ├── ext4
    │   └── lost+found  [error opening dir]
    └── find
        └── exam-files.txt                      # craeted

Print the file

    vm2 --> cat /data/find/exam-files.txt

    # result:
    /etc/exam.lsa
    /exam.lsa
    /tmp/exam.lsa
    /usr/share/exam.lsa

##### (T207, 1 pts) VM2: Create a new file based on the exam-files.txt with all words (in the file) exam changed to EXAM and store it as exam-files-upper.txt in the same folder (/data/find)

Go true the file and replace the lowcase exam with uppercase EXAM in the file and save the result in required file.

    vm2 --> sed 's/exam/EXAM/g' /data/find/exam-files.txt | sudo tee /data/find/exam-files-upper.txt

Check if the file is created and rint it

    vm2 --> tree /data

    # result:
    /data
    ├── ext4
    │   └── lost+found  [error opening dir]
    └── find
        ├── exam-files-upper.txt
        └── exam-files.txt

    vm2 --> cat /data/find/exam-files-upper.txt

    # result:
    /etc/EXAM.lsa
    /EXAM.lsa
    /tmp/EXAM.lsa
    /usr/share/EXAM.lsa

##### (T208, 2 pts) VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/lions.txt file which contains only lines that contain the lion text no matter the register (size of the letters) or position in a sentence

Check if the folder exists and if not create it

    vm2 --> tree /data/
    vm2 --> sudo mkdir -p /data/animals/

Check if the folder is created

    vm2 --> tree /data

    # result:
    /data
    ├── animals       # created
    ...

Print the file with the text tp check what sorting we need to set

    vm2 --> cat /important/animal-stories.txt

    # result:
    ...
    blue+jaguars+are+slow+and+eat+bananas
    black+crocodiles+are+slow+and+eat+oranges
    brown+whales+are+slow+and+eat+carrots
    orange+horses+are+clever+and+eat+carrots
    brown+dogs+are+good+and+eat+carrots
    blue+birds+are+blind+and+dream+bananas
    ...

Go true the file, sort the lines that contain 'lions' case unsesnsitive and save it in the required file
    
    vm2 --> cat /important/animal-stories.txt | grep -i lion | sudo tee /data/animals/lions.txt

    # result:
    yellow+lions+are+good+and+like+cucumbers
    black+lions+are+good+and+dream+apples

Check if the file is created and print it

    vm2 --> tree /data

    # result:
    /data
    ├── animals
    │   └── lions.txt

    vm2 --> cat /data/animals/lions.txt

    # result:
    yellow+lions+are+good+and+like+cucumbers
    black+lions+are+good+and+dream+apples

##### (T209, 2 pts) VM2: Create a copy of the /important/animal-stories.txt file as /data/animals/colors.txt file which contains only the unique colors in alphabetic order for all records about dogs

Check the information in the data file /important/animal-stories.txt

    vm2 --> cat /important/animal-stories.txt

    # result:
    brown+dogs+are+good+and+eat+carrots
    blue+birds+are+blind+and+dream+bananas
    white+eagles+are+blind+and+see+kiwis
    orange+pandas+are+blind+and+smell+oranges
    ...

Sort the lines with tigers

    vm2 --> cat /important/animal-stories.txt | grep dogs | cut -d '+' -f 1 | sort | uniq | sudo tee /data/animals/colors.txt

    # result:
    brown
    gray

Check if the file and its content

    vm2 --> tree /data

    # result:
    /data
    ├── animals
    │   ├── colors.txt          # created
    │   └── lions.txt

    vm2 --> cat /data/animals/colors.txt

    # result:
    brown
    gray

Connect to Vm1 and solve next task 

#### Users and Permissions - 8 tasks, 13 pts

##### (T306, 2 pts) VM2: Create a user jim with full name Jim Beam, with some password and auto-created home folder

Create user 

    vm2 --> sudo useradd -m -c 'Jim Beam' jim

Set jim password

    vm2 --> sudo passwd jim
    vm2 --> somepass
    vm2 --> somepass

##### (T307, 2 pts) VM2: Create a group named powerteam with group ID set to 2300

Create 'powerteam' group with specific ID

    vm2 --> sudo groupadd -g 2300 powerteam

##### (T308, 2 pts) VM2: Make the user jim part of the powerteam group

Set jim to be member of powergroup group

    vm2 --> sudo usermod -aG powerteam jim

Check results

    vm2 --> tail /etc/passwd

    # result:
    jim:x:1001:1001:Jim Beam:/home/jim:/bin/bash

    vm2 --> tail /etc/group

    # result:
    powerteam:x:2300:jim


Connect to VM1 and solve next task


#### Software and Services - 7 tasks, 9 pts

##### (T404, 1 pts) VM2: Install NGINX Web Server, start it, and enable it to run on boot

Update the package manager

    vm2 --> sudo dnf update

Install nginx

    vm2 --> sudo dnf install nginx
    vm2 --> y

Start and enable nginx to start on boot 

    vm2 --> sudo systemctl enable --now nginx

    # result:
    Created symlink '/etc/systemd/system/multi-user.target.wants/nginx.service' → '/usr/lib/systemd/system/nginx.service'.

Check if nginx is running

    vm2 --> systemctl status nginx

    # result:
    ● nginx.service - The nginx HTTP and reverse proxy server
        Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: disabled)
        Active: active (running) since Sun 2026-04-19 10:36:57 EEST; 7s ago
    Invocation: e7313ace5e994a8794710a189d1461f7
        Process: 15378 ExecStartPre=/usr/bin/rm -f /run/nginx.pid (code=exited, status=0/SUCCESS)
        Process: 15380 ExecStartPre=/usr/sbin/nginx -t (code=exited, status=0/SUCCESS)
        Process: 15382 ExecStart=/usr/sbin/nginx (code=exited, status=0/SUCCESS)
      Main PID: 15383 (nginx)
          Tasks: 2 (limit: 5235)
        Memory: 2.3M (peak: 2.9M)
            CPU: 40ms
        CGroup: /system.slice/nginx.service
                ├─15383 "nginx: master process /usr/sbin/nginx"
                └─15384 "nginx: worker process"

    Apr 19 10:36:57 vm2 systemd[1]: Starting nginx.service - The nginx HTTP and reverse proxy server...
    Apr 19 10:36:57 vm2 nginx[15380]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
    Apr 19 10:36:57 vm2 nginx[15380]: nginx: configuration file /etc/nginx/nginx.conf test is successful
    Apr 19 10:36:57 vm2 systemd[1]: Started nginx.service - The nginx HTTP and reverse proxy server.

##### (T405, 1 pts) VM2: Install the cowsay package and execute it with the following command cowsay 'Hello LSA(3)' > ~/cowsay.txt

Install cowsay package 

    vm2 --> sudo dnf install https://download-ib01.fedoraproject.org/pub/epel/9/Everything/x86_64/Packages/c/cowsay-3.7.0-10.el9.noarch.rpm --nogpgcheck

Execute command 'cowsay 'Hello LSA(3)' > ~/cowsay.txt'

    vm2 --> cowsay 'Hello LSA(3)' > ~/cowsay.txt

Check the result:

    vm2 --> cat ~/cowsay.txt

    # result:
     ______________
    < Hello LSA(3) >
    --------------
            \   ^__^
            \  (oo)\_______
                (__)\       )\/\
                    ||----w |
                    ||     ||


##### (T406, 1 pts) VM2: Download the appropriate package for your distribution in the home folder of the exam user:
    o For Red Hat-based and openSUSE-based distributions, download: https://zahariev.pro/linux/hello-lsa/releases/hello-lsa-1.0-1.el8.x86_64.rpm
    o For Debian-based distributions, download: https://zahariev.pro/linux/hello-lsa/releases/hello-lsa-1.0_amd64.deb

Install wget

    vm2 --> sudo dnf install wget -y

Download the appropriate package for AlmaLinux distro

    vm2 --> wget https://zahariev.pro/linux/hello-lsa/releases/hello-lsa-1.0-1.el8.x86_64.rpm

Check if it is downloaded successful

    vm2 --> ls

    # result:
    cowsay.txt  hello-lsa-1.0-1.el8.x86_64.rpm

##### (T407, 2 pts) VM2: Install the downloaded package (do not delete the downloaded file)

Install the package

    vm2 --> sudo dnf install hello-lsa-1.0-1.el8.x86_64.rpm

Test the package

    vm2 --> hello-lsa

    # result:
     _   _      _ _         _     ____    _
    | | | | ___| | | ___   | |   / ___|  / \
    | |_| |/ _ \ | |/ _ \  | |   \___ \ / _ \
    |  _  |  __/ | | (_) | | |___ ___) / ___ \
    |_| |_|\___|_|_|\___/  |_____|____/_/   \_\


Connect to VM1 and solve next task



#### Scripting and Schedules - 7 tasks, 11 pts

##### (T505, 1 pts) VM2: Create a bash script file (should contain signature at least) named symbols.sh in the /data/scripts folder

Check if /data/scripts exists and create it

    vm2 --> tree /data
    vm2 --> sudo mkdir -p /data/scripts

Check if the directory is created

    vm2 --> tree /data

Create the required script

    vm2 --> sudo vi /data/scripts/symbols.sh

```sh
#!/bin/bash
```
save the file and exit - :wq

##### (T506, 1 pts) VM2: Change permissions of the /data/scripts/symbols.sh file to executable for everyone

    vm2 --> sudo chmod -v +x /data/scripts/symbols.sh

    # result: mode of '/data/scripts/symbols.sh' changed from 0644 (rw-r--r--) to 0755 (rwxr-xr-x)

##### (T507, 3 pts) VM2: When executed the symbols.sh script should accept one parameter (if not given, should return an error and exit) and print the symbol * in a row as many times as specified by the parameter. For example, if the script is executed like this /data/scripts/symbols.sh 4 then the result will be ****

Create the commands

Create the first command for printing the stars

    vm2 --> for i in $(seq 1 5); do echo -n '*'; done; echo ''

Edit the script file and set the final script

    vm2 --> sudo vi /data/scripts/symbols.sh

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

    vm2 --> /data/scripts/symbols.sh 5

    # result:
    ****
    

[⬆ Back to top](#top)
