# Section 8 Working with Disks, File Systems and Archives 

Table of Content

- [Section 8 Working with Disks, File Systems and Archives](#section-8-working-with-disks-file-systems-and-archives)
  - [Filesystem Hierarchy Standard (FHS) - Structure and Guidelines](#filesystem-hierarchy-standard-fhs---structure-and-guidelines)
  - [Archiving Tools - Backup and Restore Techniques](#archiving-tools---backup-and-restore-techniques)
    - [Practice](#practice)
      - [Archives](#archives)
        - [tar](#tar)
        - [zip](#zip)
        - [tar gzip](#tar-gzip)
        - [tar bz2](#tar-bz2)
        - [tar xz](#tar-xz)
        - [archive results](#archive-results)
      - [unarchive archives](#unarchive-archives)
    - [from video 1:21h to 1:25h - Filesystem Hierarchy Standard (FHS) in different distros](#from-video-121h-to-125h---filesystem-hierarchy-standard-fhs-in-different-distros)
    - [from video 1:25h to 1:34h - /dev](#from-video-125h-to-134h---dev)
    - [from video 1:35h to 1:40h - /proc](#from-video-135h-to-140h---proc)
  - [Disks and Partitions Schemes - Disk Types. Partition Schemes](#disks-and-partitions-schemes---disk-types-partition-schemes)
    - [Practice](#practice-1)
  - [File Systems](#file-systems)
    - [Filesystem Types](#filesystem-types)
    - [Filesystem Tools](#filesystem-tools)
    - [Logical Volume Management - Components and Tools](#logical-volume-management---components-and-tools)
    - [RAID - Types and Tools](#raid---types-and-tools)
    - [Practice](#practice-2)


<img src="pics/lab-infrastructure.png" width="800" />
<br>
<br>

## Filesystem Hierarchy Standard (FHS) - Structure and Guidelines

[⬆ Back to top](#top)

<img src="pics/filesystem-hierarchy-standard.png" width="800" />
<br>
<br>

<img src="pics/filesystem-hierarchy-standard-1.png" width="800" />
<br>
<br>

<img src="pics/directory-classification.png" width="800" />
<br>
<br>

<img src="pics/filesystem-hierarchy-standard-2.png" width="800" />
<br>
<br>

<img src="pics/filesystem-hierarchy-standard-3.png" width="800" />
<br>
<br>

<img src="pics/filesystem-hierarchy-standard-4.png" width="800" />
<br>
<br>

<img src="pics/filesystem-hierarchy-standard-5.png" width="800" />
<br>
<br>

<img src="pics/filesystem-hierarchy-standard-6.png" width="800" />
<br>
<br>

[⬆ Back to top](#top)

## Archiving Tools - Backup and Restore Techniques

[⬆ Back to top](#top)

Archive - all files are archived in one big file with appr. the same size.
Compressed archive - all files are archived in one big file and the size is smaller then the original.

Compressed / archived files are unarchived only with the matching unarchive tool from the same pair. - zip/unzip, gzip/gunzip, xz/unxz etc.

<img src="pics/tar.png" width="800" />
<br>
<br>

tar - archive feature

<img src="pics/zip.png" width="800" />
<br>
<br>

zip - copressed archive tool

<img src="pics/unzip.png" width="800" />
<br>
<br>

unzip - unarchive compressed archives (zip)

<img src="pics/gunzip.png" width="800" />
<br>
<br>

Like zip and unzip but in GNU tools. GNU are free software fundation who develop unix tools but not only.

<img src="pics/gunzip2.png" width="800" />
<br>
<br>

<img src="pics/un-xz.png" width="800" />
<br>
<br>

<img src="pics/extra-tools.png" width="800" />
<br>
<br>

Extra tools save us severla commands to unarchive and search in the files. With this commands we can make action over archived documents.

<img src="pics/tar-extended.png" width="800" />
<br>
<br>

Most used archive tools are tar + some additional / extra tool.

### Practice

Create VM with AlmaLinux and set SSH network configuration to port 10004. We can find these configs in section 4, 5, 6 or 7.

Connect to the VM

    terminal --> ssh -p 10004 user@localhost

#### Archives

Create archive directory and go in it

    terminal --> mkdir archive
    terminal --> cd archive

Cache the user (sudo) password with sample command so we do not have to write it later

    terminal --> sudo ls /
    terminal --> user@pass

Install all tools we will use in this practice

    terminal --> sudo dnf install tar zip unzip bzip2 xz
    terminal --> y

##### tar

Create archive of /etc

    terminal --> time sudo tar -cvf etc.tar /etc && ls -alh etc.tar

    # command description
    # create tar erchive -create/verbose/filename file/archive_name target_dir and list human_readable size of the created archive

    # result:
    real    0m0.134s
    user    0m0.021s
    sys     0m0.006s
    -rw-r--r--. 1 root root 21M Apr 17 09:37 etc.tar

##### zip

Create compressed archive with zip

    terminal --> time sudo zip -ry etc.zip /etc && ls -alh etc.zip

    # command description
    # create zip compressed erchive -create_archive file/archive_name target_dir and list human_readable size of the created archive

    # result:
    real    0m5.158s      # much slower procces
    user    0m0.064s
    sys     0m0.022s
    -rw-r--r--. 1 root root 4.9M Apr 17 09:49 etc.zip     # smaller size

##### tar gzip

Create archive with tar and gzip

    terminal --> time sudo tar -czvf etc.tar.gz /etc && ls -alh etc.tar.gz

    # result:
    real    0m4.238s
    user    0m0.055s
    sys     0m0.017s
    -rw-r--r--. 1 root root 4.6M Apr 17 10:01 etc.tar.gz

##### tar bz2

Create archive with tar and bzip2

    terminal --> time sudo tar -cjvf etc.tar.bz2 /etc && ls -alh etc.tar.bz2

    # result:
    real    0m2.086s        # longer process time
    user    0m0.026s
    sys     0m0.003s
    -rw-r--r--. 1 root root 3.7M Apr 17 09:53 etc.tar.bz2       # smaller size

##### tar xz

Craete archive with tar and xz

    terminal --> time sudo tar -cJvf etc.tar.xz /etc && ls -alh etc.tar.xz

    # result:
    real    0m10.559s         # much slower archive process
    user    0m0.019s
    sys     0m0.000s
    -rw-r--r--. 1 root root 2.8M Apr 17 09:55 etc.tar.xz      # much smaller archive size

##### archive results

Show details for the archives size result.

    terminal --> ls -alhS etc*

    # result:
    -rw-r--r--. 1 root root  21M Apr 17 09:37 etc.tar
    -rw-r--r--. 1 root root 4.9M Apr 17 09:49 etc.zip
    -rw-r--r--. 1 root root 4.6M Apr 17 10:01 etc.tar.gz
    -rw-r--r--. 1 root root 3.7M Apr 17 09:53 etc.tar.bz2
    -rw-r--r--. 1 root root 2.8M Apr 17 09:55 etc.tar.xz

If we see the corelation for time and size of the archives we can see that higher archive size acheave lower size archive.

#### unarchive archives

We will unarchive archive etc.tar.gz

    terminal --> tar -xzvf etc.tar.gz

    # command description
    # tar = archive tool, -x = extract, -z = compression method, -v = verbose, -f = file, filename, current folder

    # result: automatically tar removes the slash befor etc. This prevent the critical overwrite mistake of the real /etc folder !

List current folder

    terminal --> ls -aldF etc*

    # result: 
    drwxr-xr-x. 81 user user     4096 Apr 17 09:35 etc/
    -rw-r--r--.  1 root root 21954560 Apr 17 09:37 etc.tar
    -rw-r--r--.  1 root root  3877540 Apr 17 09:53 etc.tar.bz2
    -rw-r--r--.  1 root root  4785776 Apr 17 10:01 etc.tar.gz
    -rw-r--r--.  1 root root  2909604 Apr 17 09:55 etc.tar.xz
    -rw-r--r--.  1 root root  5117681 Apr 17 09:49 etc.zip

Check differences in /etc and etc (that we unarchived). There will be no differences, but the approach is the samme in the real world.

    terminal --> diff /etc/resolv.conf etc/resolv.conf

    # no result

We will delete the archive folder

Exit the archive flder

    terminal --> cd ..

Delete the archive folder with higher access rights

    terminal --> sudo rm -rf archive/


### from video 1:21h to 1:25h - Filesystem Hierarchy Standard (FHS) in different distros
### from video 1:25h to 1:34h - /dev
### from video 1:35h to 1:40h - /proc

[⬆ Back to top](#top)


## Disks and Partitions Schemes - Disk Types. Partition Schemes

[⬆ Back to top](#top)

<img src="pics/storage-types.png" width="800" />
<br>
<br>

NAS - ready to use storage (uses ethernet protocol - standard hardware)
SAN - need preparation before usage (specialized hardware and software are needed)


<img src="pics/disk-types.png" width="800" />
<br>
<br>

<img src="pics/why-partitions.png" width="800" />
<br>
<br>

<img src="pics/measure-units.png" width="800" />
<br>
<br>

<img src="pics/masetr-boot-record.png" width="800" />
<br>
<br>

<img src="pics/guid-partition-table-gpt.png" width="800" />
<br>
<br>

<img src="pics/special-partition-categories.png" width="800" />
<br>
<br>

<img src="pics/linux-partition-codes.png" width="800" />
<br>
<br>

<img src="pics/common-partitions-and-filesystem-layouts.png" width="800" />
<br>
<br>

<img src="pics/be-cautious.png" width="800" />
<br>
<br>

<img src="pics/lsblk.png" width="800" />
<br>
<br>

<img src="pics/fdisk.png" width="800" />
<br>
<br>

<img src="pics/gdisk.png" width="800" />
<br>
<br>

<img src="pics/parted.png" width="800" />
<br>
<br>

<img src="pics/dd.png" width="800" />
<br>
<br>

<img src="pics/mkswap.png" width="800" />
<br>
<br>

<img src="pics/swapon.png" width="800" />
<br>
<br>

<img src="pics/swapoff.png" width="800" />
<br>
<br>

### Practice

Show partitions 

    terminal --> lsblk

Add storage in VM 2:51h from video
Manage disk space 2:55h from video    
    - craete partitions
    - save configs

Commands 3:00 h from video
    - dd - clone storage exactly
    - rewrite mbr with dd to simulate false disk
    - restore mbr with dd

Using gdisk 3:03h from video
    - install pepel-release
    - install gdisk
    - brake gpt tables and create new partitions
    - restore gtp tables from default backup

Manage swap memory - 3:08h from video
    - create swap partitions
    - configure swap partitions to be used

<img src="pics/name.png" width="800" />
<br>
<br>

[⬆ Back to top](#top)

## File Systems

[⬆ Back to top](#top)

### Filesystem Types

<img src="pics/what-is-a-filesystem.png" width="800" />
<br>
<br>

<img src="pics/filesystem-components.png" width="800" />
<br>
<br>

<img src="pics/filesystem-components-presented.png" width="800" />
<br>
<br>

<img src="pics/extended-filesystem.png" width="800" />
<br>
<br>

<img src="pics/journaling.png" width="800" />
<br>
<br>

<img src="pics/extended-filesystem-xfs.png" width="800" />
<br>
<br>

<img src="pics/btrfs.png" width="800" />
<br>
<br>

### Filesystem Tools

<img src="pics/mke2fs.png" width="800" />
<br>
<br>

<img src="pics/mkfs-xxx.png" width="800" />
<br>
<br>

<img src="pics/tune2fs.png" width="800" />
<br>
<br>

<img src="pics/dumpe2fs.png" width="800" />
<br>
<br>

<img src="pics/resize2fs.png" width="800" />
<br>
<br>

<img src="pics/e2fsck.png" width="800" />
<br>
<br>

<img src="pics/fsck.png" width="800" />
<br>
<br>

<img src="pics/xfs-info.png" width="800" />
<br>
<br>

<img src="pics/xfs-admin.png" width="800" />
<br>
<br>

<img src="pics/xfs-growfs.png" width="800" />
<br>
<br>

<img src="pics/xfs-repair.png" width="800" />
<br>
<br>

<img src="pics/btrfs-1.png" width="800" />
<br>
<br>

<img src="pics/mount.png" width="800" />
<br>
<br>

<img src="pics/unmount.png" width="800" />
<br>
<br>

<img src="pics/blkid.png" width="800" />
<br>
<br>

<img src="pics/tree.png" width="800" />
<br>
<br>

Swiss Knife command.

<img src="pics/mounting.png" width="800" />
<br>
<br>

Always mount filesystem in empty folder !!!

### Logical Volume Management - Components and Tools

<img src="pics/logical-volume-management-lvm.png" width="800" />
<br>
<br>

<img src="pics/pvscan.png" width="800" />
<br>
<br>

<img src="pics/pvs.png" width="800" />
<br>
<br>

<img src="pics/pvcreate.png" width="800" />
<br>
<br>

<img src="pics/vgscan.png" width="800" />
<br>
<br>

<img src="pics/vgs.png" width="800" />
<br>
<br>

<img src="pics/vgcreate.png" width="800" />
<br>
<br>

<img src="pics/vgextend.png" width="800" />
<br>
<br>

<img src="pics/lvscan.png" width="800" />
<br>
<br>

<img src="pics/lvs.png" width="800" />
<br>
<br>

<img src="pics/lvcreate.png" width="800" />
<br>
<br>

<img src="pics/lvextend.png" width="800" />
<br>
<br>

### RAID - Types and Tools

<img src="pics/raid.png" width="800" />
<br>
<br>

<img src="pics/mdadm.png" width="800" />
<br>
<br>

### Practice

Manage filesystems - 3:58 from video


<img src="pics/name.png" width="800" />
<br>
<br>

[⬆ Back to top](#top)
