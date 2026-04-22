# Section 7 System and Process Management and Monitoring 

Table of Content

- [Section 7 System and Process Management and Monitoring](#section-7-system-and-process-management-and-monitoring)
  - [A Note](#a-note)
  - [System Startup \& Boot Managers - Boot Process](#system-startup--boot-managers---boot-process)
    - [Boot Loaders - Overview. GRUB2](#boot-loaders---overview-grub2)
    - [Startup Sequence - From Boot to User Space](#startup-sequence---from-boot-to-user-space)
    - [Practice](#practice)
  - [systemd Components - Units. Targets. Dependencies](#systemd-components---units-targets-dependencies)
    - [System Initialization - Control and Monitoring](#system-initialization---control-and-monitoring)
    - [Practice](#practice-1)
    - [bash completion package](#bash-completion-package)
    - [journalctl](#journalctl)
    - [systemd](#systemd)
  - [Processes and Resources](#processes-and-resources)
    - [Processes Monitoring \& Management](#processes-monitoring--management)
    - [Resource Monitoring](#resource-monitoring)
    - [Practice](#practice-2)
      - [ps](#ps)
      - [bg - background mode](#bg---background-mode)
      - [htop](#htop)
      - [pstree](#pstree)
      - [Resources](#resources)
        - [watch](#watch)
        - [screen \& tmux - persistent sessions](#screen--tmux---persistent-sessions)
          - [screen](#screen)
          - [tmux](#tmux)


## A Note

<img src="pics/nat.png" width="800" />
<br>
<br>

<img src="pics/conf-files.png" width="800" />
<br>
<br>

<img src="pics/conf-files-1.png" width="800" />
<br>
<br>

<img src="pics/lab-infrastructure.png" width="800" />
<br>
<br>

## System Startup & Boot Managers - Boot Process

[⬆ Back to top](#top)

<img src="pics/bios-vs-uefi.png" width="800" />
<br>
<br>

<img src="pics/boot-general.png" width="800" />
<br>
<br>

### Boot Loaders - Overview. GRUB2

<img src="pics/boot-loaders.png" width="800" />
<br>
<br>

<img src="pics/grub2.png" width="800" />
<br>
<br>

<img src="pics/grub2-bios.png" width="800" />
<br>
<br>

<img src="pics/grub2-bios-deb.png" width="800" />
<br>
<br>

<img src="pics/grub2-bios-suse.png" width="800" />
<br>
<br>

<img src="pics/grub2-bios-rh.png" width="800" />
<br>
<br>

<img src="pics/grub2-uefi-deb.png" width="800" />
<br>
<br>

<img src="pics/grub2-suse.png" width="800" />
<br>
<br>

<img src="pics/default-settings.png" width="800" />
<br>
<br>

### Startup Sequence - From Boot to User Space

<img src="pics/boot-1.png" width="800" />
<br>
<br>

<img src="pics/init-methods.png" width="800" />
<br>
<br>

<img src="pics/init-methods-1.png" width="800" />
<br>
<br>

<img src="pics/systemd-components.png" width="800" />
<br>
<br>

<img src="pics/systemd-components-1.png" width="800" />
<br>
<br>

<img src="pics/dmesg.png" width="800" />
<br>
<br>

<img src="pics/efibootmgr.png" width="800" />
<br>
<br>

### Practice

To practice we need to create AlmaLinux machine from template and set SSH connection

1. Create VM from template
   
<img src="pics/import-almalinux-vm-template-1.png" width="800" />
<br>
<br>

<img src="pics/import-almalinux-vm-template-2.png" width="400" />
<br>
<br>

2. Set SSH so we can connect with more flexible terminal
   
<img src="pics/create-test-machine-and-set-ssh.png" width="800" />
<br>
<br>

Start the VM and connect with ssh

    terminal --> ssh -p 10003 user@localhost
    terminal --> yes
    terminal --> user@pass

Update dnf package manager

    terminal --> sudo dnf update
    terminal --> y

Install tree so we can check folder structure

    terminal --> sudo dnf install tree
    terminal --> user@pass

We can list the bool messages

    terminal --> sudo dmesg
    or
    terminal --> sudo dmesg -H    # more human readable

When we reset (restart) the system we can go to bios menus and we can erform different actions


<img src="pics/boot-menu.png" width="800" />
<br>
<br>

We can enter in command menu with 'e' and start the system in rescue mode with adding 'single' at the end of the 4th line 

<img src="pics/rescue-mode.png" width="800" />
<br>
<br>

Start the machine with ctrl+x. We will have to enter as root user. No other connection can be made at this point.

We can check in what mode we are in with:

    terminal --> runlevel

    # result: N 1

We can rebbot the system with:

    terminal --> reboot

After the reboot the OS will load in normal mode and we can connect with SSH again.

    terminal --> ssh -p 10003 user@localhost
    terminal --> yes
    terminal --> user@pass

If we print the run mode

    terminal --> runlevel

    # result: N 3       # this is the normal mode. More than one connection can be made.


<h3>Make permanent changes to boot process</h3>

Edit the boot config and make small changes

    terminal --> sudo vi /etc/default/grub
    terminal --> user@pass

Change the boot timeout to 10s and add 'quiet' in GRUB_CMDLINE_LINUX line

```
GRUB_TIMEOUT=10
GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"
GRUB_DEFAULT=saved
GRUB_DISABLE_SUBMENU=true
GRUB_TERMINAL_OUTPUT="console"
GRUB_CMDLINE_LINUX="resume=UUID=18076d41-ddca-4878-b91c-af069fff6c03 rd.lvm.lv=almalinux/root rd.lvm.lv=almalinux/swap quiet"
GRUB_DISABLE_RECOVERY="true"
GRUB_ENABLE_BLSCFG=true
```

Save the changes and quit the file

    terminal --> :wq!

We must generate the result files

    terminal --> sudo grub2-mkconfig -o /boot/grub2/grub.cfg --update-bls-cmdline

    # result:
    Generating grub configuration file ...
    Adding boot menu entry for UEFI Firmware Settings ...
    done

We can see the /boot directory content. initram disk one is paired with kernel on and initram disk2 is paired with kernel 2

    terminal --> sudo tree /boot
    terminal --> user@pass

    # result:
    /boot
    ├── System.map-6.12.0-124.49.1.el10_1.x86_64
    ├── System.map-6.12.0-124.8.1.el10_1.x86_64
    ├── config-6.12.0-124.49.1.el10_1.x86_64
    ├── config-6.12.0-124.8.1.el10_1.x86_64
    ├── efi
    │   └── EFI
    │       └── almalinux
    ├── grub2
    │   ├── device.map
    │   ├── fonts
    │   │   └── unicode.pf2
    │   ├── grub.cfg                # created config file
    │   ├── grubenv
    │   ├── i386-pc
    ...

    ├── initramfs-0-rescue-360c86959fd644a8b476df9f3ae1a54d.img
    ├── initramfs-6.12.0-124.49.1.el10_1.x86_64.img               # initram disk 1
    ├── initramfs-6.12.0-124.8.1.el10_1.x86_64.img                # initram disk 2
    ├── loader
    │   └── entries
    │       ├── 360c86959fd644a8b476df9f3ae1a54d-0-rescue.conf
    │       ├── 360c86959fd644a8b476df9f3ae1a54d-6.12.0-124.49.1.el10_1.x86_64.conf
    │       └── 360c86959fd644a8b476df9f3ae1a54d-6.12.0-124.8.1.el10_1.x86_64.conf
    ├── symvers-6.12.0-124.49.1.el10_1.x86_64.xz
    ├── symvers-6.12.0-124.8.1.el10_1.x86_64.xz
    ├── vmlinuz-0-rescue-360c86959fd644a8b476df9f3ae1a54d
    ├── vmlinuz-6.12.0-124.49.1.el10_1.x86_64               # kernel 1
    └── vmlinuz-6.12.0-124.8.1.el10_1.x86_64                # kernel 2

We can se the current kernel

    terminal -> uname -a

    # result: Linux localhost.localdomain 6.12.0-124.8.1.el10_1.x86_64 #1 SMP PREEMPT_DYNAMIC Tue Nov 11 11:41:04 EST 2025 x86_64 GNU/Linux

If we rebbot the VM we will see that the boot timer is 10s and we will not see that much logs when the system is booting.

    terminal --> sudo reboot
    terminal --> user@pass
  
[⬆ Back to top](#top)


## systemd Components - Units. Targets. Dependencies

[⬆ Back to top](#top)

<img src="pics/systemd-units.png" width="800" />
<br>
<br>

Good practice is to manage runtime and custom files systemd configs. If we manage the distribution installed files, when the system is updated, the configs will be overwritten. When we manage runtime and custom configs they will be not changed even when the system is updated / changed.

<img src="pics/systemd-units-types.png" width="800" />
<br>
<br>

<img src="pics/systemd-service-units.png" width="800" />
<br>
<br>

<img src="pics/systemd-target-units.png" width="800" />
<br>
<br>

<img src="pics/systemd-target-units-1.png" width="800" />
<br>
<br>

<img src="pics/systemd-units-dependencies.png" width="800" />
<br>
<br>

Soft dependancy/link - wants - units are not dependable from one another. If one of the units stops the other will continue.

Hard dependancy/link - required - if one of the units stops the other unit also stops. 

<img src="pics/systemd-unit-execution-order.png" width="800" />
<br>
<br>

<img src="pics/targets-vs-runlevel.png" width="800" />
<br>
<br>

### System Initialization - Control and Monitoring

<img src="pics/additional-systemctl-scenarios.png" width="800" />
<br>
<br>

<img src="pics/systemd-analyze.png" width="800" />
<br>
<br>

<img src="pics/journalctl.png" width="800" />
<br>
<br>

### Practice

Show currect system status

    terminal --> systemctl get-default
    terminal --> runlevel

Show all active units / targets

    terminal --> systemctl list-units --type=target

Show all units / targets

    terminal --> systemctl list-units --type=target --all

Show all active units type service

    terminal --> systemctl list-units --type=service

### bash completion package

To avoid long command writing with systemctl we will install bash completion package. This package is giving us the option to press tab and complete not only the options but also the subcommands we want to write.

    terminal --> sudo dnf install bash-completion
    terminal --> user@pass
    terminal --> y

Restart the sesson so we can enable the changes

    terminal --> exit
    terminal --> ssh -p 10003 user@localhost

Now if we wtite 'system get-' and press tab the terminal will conmplete the command to 'systemctl get-default'.

We can see options with different commands. FOr example we can see the possible options we can use:

    terminal --> systemctl list- (+ tab)

    # result:
    list-automounts    list-jobs          list-paths         list-timers        list-units
    list-dependencies  list-machines      list-sockets       list-unit-files

We can see systemctl status. The first process in our system is the initialization - init scope - systemd.

    terminal --> systemctl status

    # result:
    ● localhost.localdomain
        State: running
        Units: 319 loaded (incl. loaded aliases)
        Jobs: 0 queued
      Failed: 0 units
        Since: Thu 2026-04-16 10:34:17 CEST; 38min ago
      systemd: 257-13.el10.alma.1-gac64c15
      CGroup: /
              ├─init.scope
              │ └─1 /usr/lib/systemd/systemd --switched-root --system --deserialize=50
              ├─system.slice
              │ ├─NetworkManager.service
              │ │ └─812 /usr/sbin/NetworkManager --no-daemon
              │ ├─auditd.service
              │ │ └─761 /usr/sbin/auditd
              │ ├─chronyd.service
              │ │ └─781 /usr/sbin/chronyd -F 2
              │ ├─crond.service
              │ │ └─838 /usr/sbin/crond -n
              │ ├─dbus-broker.service
              │ │ ├─767 /usr/bin/dbus-broker-launch --scope system --audit
              │ │ └─768 dbus-broker --log 4 --controller 9 --machine-id 360c86959fd644a8b476df9f3ae1a54d --max-bytes 53687>
              │ ├─firewalld.service
              │ │ └─771 /usr/bin/python3 -sP /usr/sbin/firewalld --nofork --nopid
              │ ├─rsyslog.service
              │ │ └─860 /usr/sbin/rsyslogd -n
              │ ├─sshd.service
              │ │ └─822 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
              │ ├─system-getty.slice

If we want to see specific unit execute

    terminal --> systemctl show sshd
    or
    terminal --> systemctl cat sshd.service    # more readable


We can change system modes (not recommended in regular work)

    terminal --> sudo systemctl isolate runlevel1.target

### journalctl

First update the journal catalog

    terminal --> sudo journalctl --update-catalog
    
This feature allows us to see specific event in time. For example if we want to see most recent to older events:

    terminal --> journalctl --reverse

We can filter for specific events

    terminal --> journalctl --reverse _SYSTEMD_UNIT=sshd.service

    # result:
    Apr 16 11:26:46 localhost.localdomain sshd-session[1301]: pam_unix(sshd:session): session opened for user user(uid=1000>
    Apr 16 11:26:46 localhost.localdomain sshd-session[1301]: Accepted password for user from 10.0.2.2 port 54792 ssh2
    Apr 16 11:26:29 localhost.localdomain sshd[820]: Server listening on :: port 22.
    Apr 16 11:26:29 localhost.localdomain sshd[820]: Server listening on 0.0.0.0 port 22.

### systemd

Show the time needed for the system to get to the target status

    terminal --> systemd-analyze time

    # result:
    Startup finished in 1.120s (kernel) + 3.438s (initrd) + 7.761s (userspace) = 12.320s
    multi-user.target reached after 5.312s in userspace.

Show critical chain - the events that bring delays. We can analyze what processes are injecting delays in our system.

    terminal --> systemd-analyze critical-chain

    # result:
    The time when unit became active or started is printed after the "@" character.
    The time the unit took to start is printed after the "+" character.

    multi-user.target @5.312s
    └─rsyslog.service @5.201s +107ms
      └─network-online.target @5.189s
        └─NetworkManager-wait-online.service @4.741s +446ms     # network is with slow init
          └─NetworkManager.service @4.414s +322ms
            └─network-pre.target @4.410s
              └─firewalld.service @3.151s +1.258s               # firewall is with slow init
                └─basic.target @3.135s
                  └─dbus-broker.service @3.064s +54ms
                    └─dbus.socket @3.041s
                      └─sysinit.target @3.039s
                        └─systemd-update-utmp.service @3.018s +19ms
                          └─auditd.service @2.971s +45ms
                            └─systemd-tmpfiles-setup.service @2.697s +271ms
                              └─local-fs.target @2.665s
                                └─boot.mount @2.479s +185ms
                                  └─dev-sda2.device


Also we can follow the dependancies between units. This feature is called dot format.

    terminal --> systemd-analyze dot sshd.service

    # result:
    digraph systemd {
            "sshd.service"->"systemd-journald.socket" [color="green"];
            "sshd.service"->"ssh-host-keys-migration.service" [color="green"];
            "sshd.service"->"system.slice" [color="green"];
            "sshd.service"->"network.target" [color="green"];
            "sshd.service"->"basic.target" [color="green"];
            "sshd.service"->"sysinit.target" [color="green"];
            "sshd.service"->"sshd-keygen.target" [color="green"];
            "sshd.service"->"sysinit.target" [color="black"];
            "sshd.service"->"system.slice" [color="black"];
            "sshd.service"->"ssh-host-keys-migration.service" [color="grey66"];
            "sshd.service"->"sshd-keygen.target" [color="grey66"];
            "sshd.service"->"shutdown.target" [color="red"];
            "shutdown.target"->"sshd.service" [color="green"];
            "multi-user.target"->"sshd.service" [color="green"];
            "multi-user.target"->"sshd.service" [color="grey66"];
    }
      Color legend: black     = Requires
                    dark blue = Requisite
                    gold      = BindsTo
                    dark grey = Wants
                    red       = Conflicts
                    green     = After
    -- You probably want to process this output with graphviz' dot tool.
    -- Try a shell pipeline like 'systemd-analyze dot | dot -Tsvg > systemd.svg'!


If we want to see visuzlization we need to install dot package. We can find the name of the package in different distributions with

    terminal --> dnf provides dot

    # result:
    AlmaLinux 10 - AppStream                                                                6.1 MB/s |  15 MB     00:02
    AlmaLinux 10 - BaseOS                                                                   7.1 MB/s |  22 MB     00:03
    AlmaLinux 10 - CRB                                                                      606 kB/s | 3.4 MB     00:05
    AlmaLinux 10 - Extras                                                                    20 kB/s |  14 kB     00:00
    graphviz-9.0.0-15.el10.x86_64 : Graph Visualization Tools     # target package name
    Repo        : appstream
    Matched from:
    Filename    : /usr/bin/dot

Install the dot package

    terminal --> sudo dnf install graphviz
    terminal --> user@pass
    terminal --> y

We can use the visual pckage like saving the result of the command in .svg or png picture

    terminal --> systemd-analyze dot sshd.service | dot -Tsvg > sshd.svg
    or
    terminal --> systemd-analyze dot sshd.service | dot -Tpng > sshd.png

We can now logout from the VM , create local folder and copy the created pictures from the VM and open them.

    terminal --> logout
    terminal --> mkdir tmp
    terminal --> cd tmp
    terminal --> scp -P 10003 user@localhost:~/sshd.* .
    terminal --> user@pass

We can see the picture below

<img src="pics/unit-sshd-visalization.png" width="1000" />
<br>
<br>

We can see that we have conflict between sshd and shutdown unit because we cannot have ssh connection if we shutdown the system.

We can print sshd service, follow the dependancies and compare them with the picture

    terminal --> systemctl cat sshd.service

    # result:
    # /usr/lib/systemd/system/sshd.service
    [Unit]
    Description=OpenSSH server daemon
    Documentation=man:sshd(8) man:sshd_config(5)
    After=network.target sshd-keygen.target
    Wants=sshd-keygen.target
    # Migration for Fedora 38 change to remove group ownership for standard host keys
    # See https://fedoraproject.org/wiki/Changes/SSHKeySignSuidBit
    Wants=ssh-host-keys-migration.service

    [Service]
    Type=notify
    EnvironmentFile=-/etc/sysconfig/sshd
    ExecStart=/usr/sbin/sshd -D $OPTIONS
    ExecReload=/bin/kill -HUP $MAINPID
    KillMode=process
    Restart=on-failure
    RestartSec=42s

    [Install]
    WantedBy=multi-user.target

Compare dependancies as on the picture:

<img src="pics/unit-sshd-visalization.png" width="1000" />
<br>
<br>

We can also create the same visual representation for systemd

    terminal --> systemd-analyze plot > systemd.svg
    terminal --> exit
    terminal --> scp -P 10003 user@localhost:~/systemd.svg .
    terminal --> user@pass

<img src="pics/systemd-svg-present.png" width="800" />
<br>
<br>

<img src="pics/systemd-svg-present-1.png" width="800" />
<br>
<br>

<img src="pics/systemd-svg-present-2.png" width="800" />
<br>
<br>

<img src="pics/systemd-svg-present-3.png" width="800" />
<br>
<br>

<img src="pics/systemd-svg-present-4.png" width="800" />
<br>
<br>

[⬆ Back to top](#top)


## Processes and Resources

[⬆ Back to top](#top)

### Processes Monitoring & Management

<img src="pics/processes-and-jobs.png" width="800" />
<br>
<br>

<img src="pics/jobs.png" width="800" />
<br>
<br>

<img src="pics/fg.png" width="800" />
<br>
<br>

<img src="pics/bg.png" width="800" />
<br>
<br>

<img src="pics/ps.png" width="800" />
<br>
<br>

<img src="pics/pstree.png" width="800" />
<br>
<br>

<img src="pics/pgrep.png" width="800" />
<br>
<br>

<img src="pics/top.png" width="800" />
<br>
<br>

<img src="pics/htop.png" width="800" />
<br>
<br>

<img src="pics/common-sugnals.png" width="800" />
<br>
<br>

<img src="pics/kill.png" width="800" />
<br>
<br>

<img src="pics/kill-all.png" width="800" />
<br>
<br>

<img src="pics/pkill.png" width="800" />
<br>
<br>

<img src="pics/process-priorities.png" width="800" />
<br>
<br>

<img src="pics/process-priorities-1.png" width="800" />
<br>
<br>

<img src="pics/nice.png" width="800" />
<br>
<br>

<img src="pics/renice.png" width="800" />
<br>
<br>

<img src="pics/watch.png" width="800" />
<br>
<br>

<img src="pics/nogup.png" width="800" />
<br>
<br>

We start a process in background and they are working even if we close the connection session.

<img src="pics/screen.png" width="800" />
<br>
<br>

We create as session that is persistent even if the connection is lost and after the connection is established again we can enter the working persistent session. For example long process of compliation.

<img src="pics/tmux.png" width="800" />
<br>
<br>

This program is similar to screen - for persistant sessions.

### Resource Monitoring

<img src="pics/free.png" width="800" />
<br>
<br>

<img src="pics/df.png" width="800" />
<br>
<br>

<img src="pics/du.png" width="800" />
<br>
<br>

What folder how much space is taking.

<img src="pics/vmstat.png" width="800" />
<br>
<br>

Show virtual memory statistics - sum of operation memory and swap memory. Swap memory is taken from processes that are not using it and temporary set as required of currently running process the nswaped back.

<img src="pics/iostat.png" width="800" />
<br>
<br>

<img src="pics/pidstat.png" width="800" />
<br>
<br>

<img src="pics/sar.png" width="800" />
<br>
<br>

<img src="pics/iotop.png" width="800" />
<br>
<br>

<img src="pics/nmon.png" width="800" />
<br>
<br>

<img src="pics/lsof.png" width="800" />
<br>
<br>

### Practice

#### ps

We ca nstart ping to localhost and pause it after few seconds

    terminal --> ping localhost
    pause - ctrl + z

Now we can list running processes in the current session

    terminal --> ps lf

    # result:
    F   UID     PID    PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
    0  1000    2304    2303  20   0   5592  4796 do_wai Ss   pts/0      0:00 -bash
    0  1000    2334    2304  20   0   4912  2596 do_sig T    pts/0      0:00  \_ ping localhost
    0  1000    2339    2304  20   0   6660  3668 -      R+   pts/0      0:00  \_ ps lf

Show manual for ps

    terminal --> man ps


Start process watch - top and pause it after few seconds

    terminal --> top
    pause - ctrl + z

Now we can list curent jobs and see paused/stopped jobs. The '+' sign next to the job id shows if the job is the last we interacted with.

    terminal --> jobs

    # result:
    [1]-  Stopped                 ping localhost
    [2]+  Stopped                 top

Now if we use foreground command - fg, the last job will be resumed and visualized.

    terminal --> fg

We can foreground job with specific id - for example the ping process. The ping will start and continue on foreground.

    terminal --> fg 1

If now we list jobs, the last job will be the ping

    terminal --> jobs

    # result:
    [1]+  Stopped                 ping localhost            # last used
    [2]-  Stopped                 top

We cam list jobs with details - process id parent process id, niceness, 

    terminal --> ps lf

    # result:
    F   UID     PID    PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
    0  1000    2304    2303  20   0   5592  4800 do_wai Ss   pts/0      0:00 -bash
    0  1000    2334    2304  20   0   4912  2596 do_sig T    pts/0      0:00  \_ ping localhost
    0  1000    2357    2304  20   0   7644  5344 do_sig T    pts/0      0:00  \_ top
    0  1000    2368    2304  20   0   6660  3688 -      R+   pts/0      0:00  \_ ps lf


#### bg - background mode

If we use only command bg, the last job we worked with will appear on the console and we can use the console but the output of our commands will be mixed with the ping job. To stop this mode we must use fg command to take the job in foreground and then stop or pause it. If another job come current and the ping is still running we can stop the foreground job with 'q' and then use again 'fg' command to set the ping job as current and then stop it with 'q'. We have stopped all jobs and if we list jobs we will receive empty result.

To set the ping job or any other job in background mode wihout interacting with our work we must use '&' at the end of the command and save the output somwhere we can see it later. As result we receive process ID

    terminal --> ping localhost > /tmp/pingout.txt &

    # result:
    [1] 2380

We can list processes and see the started job

    terminal --> ps -l

    # result:
    F S   UID     PID    PPID  C PRI  NI ADDR SZ WCHAN  TTY          TIME CMD
    0 S  1000    2304    2303  0  80   0 -  1398 do_wai pts/0    00:00:00 bash
    0 S  1000    2380    2304  0  80   0 -  1228 skb_wa pts/0    00:00:00 ping      # ping is running
    0 R  1000    2381    2304  0  80   0 -  1665 -      pts/0    00:00:00 ps

We can still look at the process latest information with command 'tail' and stop the following with ctrl + c but the job is still working.

    terminal --> tail -f /tmp/pingout.txt

We can kill the job in few ways. First we can kill group of jobs.

    terminal --> pkill ping

Another way is to find the jobs IDs and the use them to kill the specific jobs.

Start 2 sleep jobs

    terminal --> sleep 1d &         # [2] 2388
    terminal --> sleep 1200 &       # [3] 2389

Find the jobs IDs

    terminal --> pgrep sleep 

    # result:
    2388
    2389

Kill the jobs with 'kill' command. 'pkill' is working only with names!

    terminal --> kill $(pgrep sleep)

    # result:
    [2]-  Terminated              sleep 1d
    [3]+  Terminated              sleep 1200 


#### htop

Install htop command

    terminal --> sudo dnf install epel-release
    terminal --> y
    terminal --> sudo dnf install htop
    terminal --> y
    terminal --> y

Using htop. F5 can set the output as a tree.

    terminal --> htop

<img src="pics/htop-tree.png" width="800" />
<br>
<br>


#### pstree

Another useful command that we can install additionally.

Find the name of the package in the used distribution

    terminal --> dnf provides pstree

    # result:
    Extra Packages for Enterprise Linux 10 - x86_64                                         3.4 MB/s |  16 MB     00:04
    Last metadata expiration check: 0:00:07 ago on Thu Apr 16 13:08:32 2026.
    psmisc-23.6-8.el10.x86_64 : Utilities for managing processes on your system
    Repo        : @System
    Matched from:
    Filename    : /usr/bin/pstree

    psmisc-23.6-8.el10.x86_64 : Utilities for managing processes on your system
    Repo        : baseos
    Matched from:
    Filename    : /usr/bin/pstree

Install pstree

    terminal --> sudo dnf install psmisc
    terminal --> user@pass

Start 2 sleep jobs

    terminal --> sleep 1d &             # [2] 2525
    terminal --> sleep 1800 &           # [3] 2526

List jobs

    terminal --> ps al

    # result:
    F   UID     PID    PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
    4     0     838       1  20   0   4972  2388 -      Ss+  tty1       0:00 /sbin/agetty -o -- \u --noreset --noclear - lin
    0  1000    2304    2303  20   0   5724  4944 do_wai Ss   pts/0      0:00 -bash
    0  1000    2380    2304  20   0   4912  2460 skb_wa S    pts/0      0:00 ping localhost
    0  1000    2525    2304  20   0   2880  1876 hrtime S    pts/0      0:00 sleep 1d
    0  1000    2526    2304  20   0   2880  1812 hrtime S    pts/0      0:00 sleep 1800
    0  1000    2528    2304  20   0   6660  3640 -      R+   pts/0      0:00 ps al

Use pstree to draw a tree for the bash process using his PID (2304)

    terminal --> pstree 2304

    # result:
    bash─┬─ping
         ├─pstree
         └─2*[sleep]

We can also see the tree for all our processes

    terminal --> pstree
    
    # result:
    systemd─┬─NetworkManager───3*[{NetworkManager}]
            ├─agetty
            ├─auditd───{auditd}
            ├─chronyd
            ├─crond
            ├─dbus-broker-lau───dbus-broker
            ├─firewalld───{firewalld}
            ├─rsyslogd───2*[{rsyslogd}]
            ├─sshd───sshd-session───sshd-session───bash─┬─pstree
            │                                           └─2*[sleep]
            ├─systemd───(sd-pam)
            ├─systemd-journal
            ├─systemd-logind
            ├─systemd-udevd
            └─systemd-userdbd───3*[systemd-userwor]


Wecan list processes and ther hierarchy. We can follow each process parent and children processes.

    terminal --> ps axl

    # result:
    F   UID     PID    PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
    4     0       1       0  20   0  49128 40776 -      Ss   ?          0:04 /usr/lib/systemd/systemd --switched-root --syst
    1     0       2       0  20   0      0     0 -      S    ?          0:00 [kthreadd]
    1     0       3       2  20   0      0     0 -      S    ?          0:00 [pool_workqueue_release]
    1     0       4       2   0 -20      0     0 -      I<   ?          0:00 [kworker/R-rcu_gp]
    1     0       5       2   0 -20      0     0 -      I<   ?          0:00 [kworker/R-sync_wq]
    1     0       6       2   0 -20      0     0 -      I<   ?          0:00 [kworker/R-slub_flushwq]
    1     0       7       2   0 -20      0     0 -      I<   ?          0:00 [kworker/R-netns]
    1     0      10       2   0 -20      0     0 -      I<   ?          0:00 [kworker/0:0H-kblockd]
    1     0      13       2   0 -20      0     0 -      I<   ?          0:00 [kworker/R-mm_percpu_wq]
    1     0      14       2  20   0      0     0 -      I    ?          0:00 [rcu_tasks_kthread]
    1     0      15       2  20   0      0     0 -      I    ?          0:00 [rcu_tasks_rude_kthread]
    1     0      16       2  20   0      0     0 -      I    ?          0:00 [rcu_tasks_trace_kthread]
    1     0      17       2  20   0      0     0 -      S    ?          0:00 [ksoftirqd/0]
    1     0      18       2  20   0      0     0 -      I    ?          0:00 [rcu_preempt]
    1     0      19       2  20   0      0     0 -      S    ?          0:00 [rcu_exp_par_gp_kthread_worker/0]
    1     0      20       2  20   0      0     0 -      S    ?          0:00 [rcu_exp_gp_kthread_worker]
    1     0      21       2 -100  -      0     0 -      S    ?          0:00 [migration/0]
    1     0      22       2 -51   -      0     0 -      S    ?          0:00 [idle_inject/0]

We can filter specific process by id (2)

    terminal --> ps -fp 2

    # re sult:
    UID          PID    PPID  C STIME TTY          TIME CMD
    root           2       0  0 11:26 ?        00:00:00 [kthreadd]

We can increatse niceness of specific process by id. This mean that the priority also increase and this means that the process is getting less cpu to operate with.

Find the proces id - PID

    terminal --> ps l

    # result:
    F   UID     PID    PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
    0  1000    2304    2303  20   0   5724  4944 do_wai Ss   pts/0      0:00 -bash
    0  1000    2525    2304  20   0   2880  1876 hrtime S    pts/0      0:00 sleep 1d   # target process
    0  1000    2736    2304  20   0   6660  3748 -      R+   pts/0      0:00 ps l

Increase process niceness

    terminal --> renice 10 2525

    # result: 2525 (process ID) old priority 0, new priority 10

List proceses again

    terminal --> ps l

    # result:
    F   UID     PID    PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
    0  1000    2304    2303  20   0   5724  4944 do_wai Ss   pts/0      0:00 -bash
    0  1000    2525    2304  30  10   2880  1876 hrtime SN   pts/0      0:00 sleep 1d # NI and PRI changed
    0  1000    2739    2304  20   0   6660  3744 -      R+   pts/0      0:00 ps l

If we want ot decrease niceness of specific process we need to have higher access level

    terminal --> sudo renice 0 2525
    terminal --> user@pass

    # result: 2525 (process ID) old priority 10, new priority 0

List processes again

    terminal --> ps l

    # result:
    F   UID     PID    PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
    0  1000    2304    2303  20   0   5724  4944 do_wai Ss   pts/0      0:00 -bash
    0  1000    2525    2304  20   0   2880  1876 hrtime S    pts/0      0:00 sleep 1d # normalized process
    0  1000    2736    2304  20   0   6660  3748 -      R+   pts/0      0:00 ps l

Kill all sleep jobs

    terminal --> pkill sleep

#### Resources

Show process resources in human readable foramt 

    terminal --> free -h

    # result:
                   total        used        free      shared  buff/cache   available
    Mem:           1.7Gi       387Mi       908Mi       4.8Mi       557Mi       1.3Gi    # operation memory
    Swap:          2.0Gi          0B       2.0Gi                                        # swap memory

We wnat not to use swap memory because the speed of disk space as memory is slower than the operation memory.

List disk sizes

    terminal --> df -h

    # result:
    Filesystem                  Size  Used Avail Use% Mounted on
    /dev/mapper/almalinux-root   29G  1.9G   28G   7% /
    devtmpfs                    833M     0  833M   0% /dev
    tmpfs                       853M     0  853M   0% /dev/shm
    tmpfs                       342M  4.8M  337M   2% /run
    tmpfs                       1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
    /dev/sda2                   960M  296M  665M  31% /boot
    tmpfs                       1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
    tmpfs                       171M  4.0K  171M   1% /run/user/1000

Show utiliztion of directory

    terminal --> sudo du -h -s /etc         # du = directory utilization, -h = human readable, -s = summary

    # result: 22M     /etc

We can list each object in specific folder, sorted by human readable values - size utilized

    terminal --> sudo du -h -s /etc/* | sort -h

##### watch 

Watch specific background process

Start temporary process

    terminal --> for i in $(seq 1 100); do echo "Progress: $i" > /tmp/a.txt; sleep 3; done &

Start watching the process

    terminal --> watch -n 5 cat /tmp/a.txt

This way we can watch background process without interupting

##### screen & tmux - persistent sessions

###### screen

INstall screen and tmux

    terminal --> sudo dnf install screen tmux

Give permissions to screen dir

    terminal --> sudo chmod -Rv 777 /run/screen

    # result: mode of '/run/screen' changed from 0775 (rwxrwxr-x) to 0777 (rwxrwxrwx)

Start screen session

    terminal --> screen

Show process tree to view active sessions. We have double screen in one branch. One of the 'scrren' is the command and the other one is the session. After the screen we have separate bash session which is the current session.

    termiinal --> pstree

    # result:
    systemd─┬─NetworkManager───3*[{NetworkManager}]
            ├─agetty
            ├─auditd───{auditd}
            ├─chronyd
            ├─crond
            ├─dbus-broker-lau───dbus-broker
            ├─firewalld───{firewalld}
            ├─rsyslogd───2*[{rsyslogd}]
            ├─sshd───sshd-session───sshd-session───bash───screen───screen───bash───pstree
            ├─systemd───(sd-pam)
            ├─systemd-journal
            ├─systemd-logind
            ├─systemd-udevd
            └─systemd-userdbd───3*[systemd-userwor]


Start temporary process with for cycle in the screen session in foreground

    terminal --> for i in $(seq 1 1000); do echo "Progress: $i"; sleep 5; done 

The process is now working in foreground. 

Disattach with 'ctrl + a + d' and list the process tree again. We can see that the screen session is still available.

    terminal --> pstree

    # result:
    systemd─┬─NetworkManager───3*[{NetworkManager}]
            ├─agetty
            ├─auditd───{auditd}
            ├─chronyd
            ├─crond
            ├─dbus-broker-lau───dbus-broker
            ├─firewalld───{firewalld}
            ├─rsyslogd───2*[{rsyslogd}]
            ├─screen───bash───sleep
            ├─sshd───sshd-session───sshd-session───bash───pstree
            ├─systemd───(sd-pam)
            ├─systemd-journal
            ├─systemd-logind
            ├─systemd-udevd
            └─systemd-userdbd───3*[systemd-userwor]

We can also close the session with the VM and then connect again and call the screen command we will see that we have one running session.

    termimnal --> exit
    terminal --> ssh -p 10003 user@localhost
    terminal --> user@pass

    terminal --> screen

    # result:
    There is a screen on:
        2986.pts-0.localhost    (Detached)
    1 Socket in /run/screen/S-user.

We can flllow parent-child process and see what exactly we are connecting to. 2986 is the parent of the sleep process which is child of the screen session.

    terminal --> ps l

    # result:
    F   UID     PID    PPID PRI  NI    VSZ   RSS WCHAN  STAT TTY        TIME COMMAND
    0  1000    2987    2986  20   0   5740  4944 do_wai Ss   pts/1      0:00 /bin/bash
    0  1000    3067    3066  20   0   5592  4844 do_wai Ss   pts/0      0:00 -bash
    0  1000    3189    2987  20   0   2880  1824 hrtime S+   pts/1      0:00 sleep 5
    0  1000    3190    3067  20   0   6660  3680 -      R+   pts/0      0:00 ps l

We can attach again to this screen session

    terminal --> screen -r 2986

Stop the screen process - ctrl + c

Exit the screen session

    terminal --> exit

List screen session to see that hte screen session is terminated

    terminal --> screen -ls

    # result: No Sockets found in /run/screen/S-user.


###### tmux

Start tmux session

    terminal --> tmux

Start temporary process in tmux session

    terminal --> for i in $(seq 1 1000); do echo "Progress: $i"; sleep 5; done 

Detach from tmux session with ctrl + b, d

List tmux sessions. This will show sessions and their windows. In one tmux sessions we can have more than one window.

    terminal --> tmux ls

    # result: 
    0: 1 windows (created Thu Apr 16 17:26:52 2026)

Exit the VM to close the session, connect again and list tmmux sessions. We will see that we still have active tmux session.

    terminal --> exit
    terminal --> ssh -p 10003 user@localhost

    terminal --> tmux ls

    # result:
    0: 1 windows (created Thu Apr 16 17:26:52 2026)

Reattach to tmux session

    terminal --> tmux attach-session -t 0

Stop the process - ctrl + c

Exit the session

    terminal --> exit

Check that the tmux session is closed

    terminal --> tmux ls

    # result: no server running on /tmp/tmux-1000/default

[⬆ Back to top](#top)



