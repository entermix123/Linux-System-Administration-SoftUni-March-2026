# Section 6 Network, Software and Services Management 

Table of Contents

- [Section 6 Network, Software and Services Management](#section-6-network-software-and-services-management)
  - [Network and Services](#network-and-services)
    - [Network Fundamentals - Basics. OSI vs TCP. IP Addressing](#network-fundamentals---basics-osi-vs-tcp-ip-addressing)
    - [Network Device Naming In Modern Linux Distributions](#network-device-naming-in-modern-linux-distributions)
    - [Network Stack - Configuration and Testing](#network-stack---configuration-and-testing)
    - [Services Control - Manage Services with systemctl](#services-control---manage-services-with-systemctl)
    - [Practice](#practice)
  - [Software Management](#software-management)
    - [Package Management - Local Packages and RPM](#package-management---local-packages-and-rpm)
    - [Package Management - Repositories and YUM/DNF](#package-management---repositories-and-yumdnf)
    - [Package Management - Repositories and zypper](#package-management---repositories-and-zypper)
    - [Package Management - Local Packages and dpkg](#package-management---local-packages-and-dpkg)
    - [Package Management - Repositories and apt/apt-\*](#package-management---repositories-and-aptapt-)
    - [Software Management - Alternative (Universal) Package Formats](#software-management---alternative-universal-package-formats)
    - [Practice](#practice-1)
  - [Basic Network Services](#basic-network-services)
    - [Secure Shell (SSH) Introduction](#secure-shell-ssh-introduction)
    - [Dynamic Host Configuration Protocol Introduction](#dynamic-host-configuration-protocol-introduction)
    - [Practice](#practice-2)


<img src="pics/lab-infrastructure.png" width="800" />
<br>
<br>

## Network and Services

[⬆ Back to top](#top)

### Network Fundamentals - Basics. OSI vs TCP. IP Addressing

<img src="pics/network-models.png" width="800" />
<br>
<br>

<img src="pics/network-protocols.png" width="800" />
<br>
<br>

<img src="pics/ports-numbers.png" width="800" />
<br>
<br>

<img src="pics/ip-generals.png" width="800" />
<br>
<br>

<img src="pics/ipv4-rules.png" width="800" />
<br>
<br>

<img src="pics/ipv4-class-address.png" width="800" />
<br>
<br>

<img src="pics/ipv4-special-addresses.png" width="800" />
<br>
<br>

<img src="pics/ipv4-special-addresses-1.png" width="800" />
<br>
<br>

<img src="pics/ipv4-addresses-standartd-mask.png" width="800" />
<br>
<br>

<img src="pics/ipv4-addresses-non-standartd-mask.png" width="800" />
<br>
<br>

<img src="pics/network-naming-scheme-1.png" width="800" />
<br>
<br>

### Network Device Naming In Modern Linux Distributions

<img src="pics/network-naming-scheme-1.png" width="800" />
<br>
<br>

<img src="pics/network-naming-rules.png" width="800" />
<br>
<br>


### Network Stack - Configuration and Testing

<img src="pics/network-stack-general.png" width="800" />
<br>
<br>

<img src="pics/network-stack-general-1.png" width="800" />
<br>
<br>


<img src="pics/network-stack-option-1.png" width="800" />
<br>
<br>

<img src="pics/network-stack-option-2.png" width="800" />
<br>
<br>

<img src="pics/network-stack-option-3.png" width="800" />
<br>
<br>

<img src="pics/netplan.png" width="800" />
<br>
<br>

<img src="pics/ip.png" width="800" />
<br>
<br>

<img src="pics/nmcli.png" width="800" />
<br>
<br>

<img src="pics/nmtui.png" width="800" />
<br>
<br>

<img src="pics/networkctl.png" width="800" />
<br>
<br>

<img src="pics/wicked.png" width="800" />
<br>
<br>

<img src="pics/ping.png" width="800" />
<br>
<br>

<img src="pics/arp.png" width="800" />
<br>
<br>

arp give us the connection between MAC address and IP address of the specific device.

<img src="pics/arping.png" width="800" />
<br>
<br>

### Services Control - Manage Services with systemctl

<img src="pics/systemctl.png" width="800" />
<br>
<br>

<img src="pics/common-systemctl-scenarios.png" width="800" />
<br>
<br>

<img src="pics/common-systemctl-scenarios-1.png" width="800" />
<br>
<br>

With systemctl we can manage the systemd component - metwork services.

### Practice

1:35h from video - setting up linux network configs in virtualbox

Set internal network configuration

<img src="pics/host-internal-network-settings.png" width="800" />
<br>
<br>

Set SSH configs

<img src="pics/ssh-server-configs.png" width="800" />
<br>
<br>

Make ssh connection with the AlmaLinux VM

- regenerate ssh key if needed      
    terminal --> ssh-keygen -R "[localhost]:10002"

- Connect to the VM     
    terminal --> ssh -p 10002 user@localhost

Rename the machine so we know on which machine we are working

    terminal --> sudo hostnamectl set-hostname jupiter.sla.lab
    terminal --> user@pass

    Check the set name

        terminal --> cat /etc/hostname

Set pretty (descriptional) name

    terminal --> sudo hostnamectl set-hostname --pretty 'Jupiter Server'
    terminal --> user@pass

    Check the set pretty name

        terminal --> cat /etc/machine-info

Exit and reconnect to the machine to enable changes

    terminal --> exit
    terminal --> ssh -p 10002 user@localhost

    # result:
    [user@jupiter ~]$

Show network adapters

    terminal --> ip link show

    # result:

<img src="pics/show-network-adapters.png" width="800" />
<br>
<br>

LO - loop back adapter - not virtual or phisical device

Turn off specific network adapter

    terminal --> sudo ip link set dev enp0s8 down

    # result:

<img src="pics/turn-off-network-adapter.png" width="800" />
<br>
<br>

Turn on specific network adapter

    terminal --> sudo ip link set dev enp0s8 up

    # result:

<img src="pics/turn-on-network-adapter.png" width="800" />
<br>
<br>

List IP addresses

    terminal --> ip address show

    # result:

<img src="pics/list-ip-address.png" width="800" />
<br>
<br>

Set temporary IP address of spceific network adapter - enp0s8 from the last picture. After few minutes this IP will be cleared. This is because the network manager is setting the addresses dynamically and this is manually set address.

    terminal --> sudo ip address add 192.168.200.1/24 dev enp0s8

    # result:

<img src="pics/temporary-ip-address.png" width="800" />
<br>
<br>

How to set permanent IP address - with network manager. We can list the network configurations of the current OS with network manager cli:

    terminal --> nmcli general status

And we can list the connections of the network devices

    terminal --> nmcli connection show

    # result:
    
<img src="pics/network-info.png" width="800" />
<br>
<br>

We have few separations of used words
- link - phisical cable connection
- connection - network configurations


We wil remove the configurations for the Wired connection 1 and list the config again to see that the configuration is removed and the network device is still avalable.

    terminal --> sudo nmcli connection de; "Wired connection 1"

    terminal --> ip link show

    # result:

<img src="pics/remove-connection-configs.png" width="800" />
<br>
<br>

We will create custom configuration and list the connection to confirm the results

    terminal --> sudo nmcli connection add type ethernet ifname enp0s8 con-name static-internal

    terminal --> ip link show

    # result

<img src="pics/create-connection-config.png" width="800" />
<br>
<br>

Good practice is to name the configuration with the adapter name, but we can set whatever name we want.

We can print the configuration we created

    terminal --> ls -la /etc/NetworkManager/system-connections/static-internal.nmconnection

    # result:

<img src="pics/print-connection-config.png" width="800" />
<br>
<br>

But in the picture we don't have filled details, because the there is no dynamic host (DHCP) to set the configs automatically. This is why the connection is in different color.

We will set the manual method to set the netwrok configs for permanent IP address

    terminal --> sudo nmcli connection modify static-internal ipv4.addresses 192.168.200.1/24 ipv4.method manual

Restart the configuration so the network manager can process the situation quickly

    terminal --> sudo nmcli connection down static-internal; sudo nmcli connection up static-internal

After we list the connections again the created connection is green like the other ones.

<img src="pics/connnection-ready.png" width="800" />
<br>
<br>

When we print the network adapters we can see that the adapter we configured have an IP address

<img src="pics/permanent-ip-address.png" width="800" />
<br>
<br>

When we list the connection configuration we will see that the config are different

    terminal --> ls -la /etc/NetworkManager/system-connections/static-internal.nmconnection

    # result:

<img src="pics/connection-configs.png" width="800" />
<br>
<br>

We can use psevdo user interface

    terminal --> nmtui

    # result:

<img src="pics/nmtui-ui.png" width="400" />
<br>
<br>

<img src="pics/nmtui-ui-1.png" width="400" />
<br>
<br>

<img src="pics/nmtui-ui-3.png" width="600" />
<br>
<br>

<img src="pics/nmtui-ui-2.png" width="600" />
<br>
<br>

1.48h - 1.58h from video - debian and opensuse configs

[⬆ Back to top](#top)


## Software Management

[⬆ Back to top](#top)

<img src="pics/apps-libraries.png" width="800" />
<br>
<br>

<img src="pics/static-vs-dynamic-links.png" width="800" />
<br>
<br>

<img src="pics/packages-are-solutions.png" width="800" />
<br>
<br>

<img src="pics/packages-are-solutions-1.png" width="800" />
<br>
<br>

<img src="pics/rpm.png" width="800" />
<br>
<br>

<img src="pics/deb.png" width="800" />
<br>
<br>

<img src="pics/ldd.png" width="800" />
<br>
<br>

### Package Management - Local Packages and RPM

<img src="pics/rpm-database.png" width="800" />
<br>
<br>

<img src="pics/rpm-package-files.png" width="800" />
<br>
<br>

<img src="pics/rpm-package-files-1.png" width="800" />
<br>
<br>

<img src="pics/rpm-commands.png" width="800" />
<br>
<br>

<img src="pics/common-rpm-scenarios.png" width="800" />
<br>
<br>

<img src="pics/common-rpm-scenarios-1.png" width="800" />
<br>
<br>

<img src="pics/common-rpm-scenarios-2.png" width="800" />
<br>
<br>

### Package Management - Repositories and YUM/DNF

<img src="pics/yum-dnf.png" width="800" />
<br>
<br>

<img src="pics/common-yum-dnf-scenarios.png" width="800" />
<br>
<br>

<img src="pics/common-yum-dnf-scenarios-1.png" width="800" />
<br>
<br>

<img src="pics/common-yum-dnf-scenarios-2.png" width="800" />
<br>
<br>

<img src="pics/common-yum-dnf-scenarios-3.png" width="800" />
<br>
<br>

<img src="pics/install-epel-repo.png" width="800" />
<br>
<br>

### Package Management - Repositories and zypper

<img src="pics/zypper.png" width="800" />
<br>
<br>

<img src="pics/common-zypper-scenarios.png" width="800" />
<br>
<br>

<img src="pics/common-zypper-scenarios-1.png" width="800" />
<br>
<br>

<img src="pics/common-zypper-scenarios-2.png" width="800" />
<br>
<br>

<img src="pics/common-zypper-scenarios-3.png" width="800" />
<br>
<br>

### Package Management - Local Packages and dpkg

<img src="pics/deb-db.png" width="800" />
<br>
<br>

<img src="pics/deb-packages-files.png" width="800" />
<br>
<br>

<img src="pics/deb-packages-files-1.png" width="800" />
<br>
<br>

<img src="pics/common-dpkg-scenarios.png" width="800" />
<br>
<br>

<img src="pics/common-dpkg-scenarios-1.png" width="800" />
<br>
<br>

### Package Management - Repositories and apt/apt-*

<img src="pics/apt.png" width="800" />
<br>
<br>

<h3>Good practice is when in interactive mode we use apt (the most higher package manager) but in scripts we use the individual apt tools.</h3>

<img src="pics/common-apt-scenarios.png" width="800" />
<br>
<br>

<h3>Updating  the package repositories are different in RPM and DEB package managers.</h3>      
<h3>- With RPM package manager the repositories update is executed automatically with the last rpm command.</h3>
<h3>- With DEB package manager the repositories are updated manually or in scheduled activity but not included in the package installation process.</h3>

<img src="pics/common-apt-scenarios-1.png" width="800" />
<br>
<br>

<img src="pics/apt-tools.png" width="800" />
<br>
<br>

<h3>Here are the apt tools we use in script development.</h3>

<img src="pics/common-apt-scenarios-3.png" width="800" />
<br>
<br>

<img src="pics/common-apt-scenarios-2.png" width="800" />
<br>
<br>

<img src="pics/common-apt-scenarios-4.png" width="800" />
<br>
<br>

### Software Management - Alternative (Universal) Package Formats

<img src="pics/brief-comparison.png" width="800" />
<br>
<br>

### Practice

<h3>AlmaLinux Examples:</h3>

Update packages 

    terminal --> sudo dnf upgrade

    # result:

<img src="pics/dnf-upgrade.png" width="800" />
<br>
<br>

<img src="pics/dnf-upgrade-1.png" width="800" />
<br>
<br>

Find wget package

    terminal --> dnf search wget

    # result:

<img src="pics/dnf-wget-search.png" width="800" />
<br>
<br>

Install wget package

    terminal --> sudo dnf install wget

    # result:

<img src="pics/dnf-install-wget.png" width="800" />
<br>
<br>

<img src="pics/dnf-install-wget-1.png" width="800" />
<br>
<br>

List package repositories and their folders

    terminal --> dnf repolist

    terminal --> ls -al /etc/yum.repos.d/

<img src="pics/dnf-list-repos-and-dirs.png" width="800" />
<br>
<br>

Some of the packages can participate in few or several repos (for main repo, source code, debug info etc.). We can list all repositories and check who of them are enabled.

    terminal --> dnf repolist --all

    # result:

<img src="pics/dnf-repo-list-all.png" width="800" />
<br>
<br>

We can activate specific repository if we need to use it.

    terminal --> sudo dnf config-manager --enable highavailability

    # result:

<img src="pics/dnf-enable-repo-example.png" width="800" />
<br>
<br>

Install the most used repository - epel

    terminal --> sudo dnf install -y epel-release

    # result:

<img src="pics/dnf-install-epel.png" width="800" />
<br>
<br>

<img src="pics/dnf-install-epel-1.png" width="800" />
<br>
<br>

We can list and print some of the repositories files on the console

    terminal --> cat /etc/yum.repos.d/epel.repo

    # result:

<img src="pics/dnf-epel-print.png" width="800" />
<br>
<br>

There are cases that we should write manually add configuration block in the repository files. One of these cases are using Docker or other specific software. These blocks are usually provided in the software installation instructions for the specific OS.

<h3>from 3.00h to 3.17h - OpenSuse and Debian examples.</h3>


[⬆ Back to top](#top)

## Basic Network Services

[⬆ Back to top](#top)

<h3>In AlmaLinux (Red Hat) and OpenSUse we have active firewall but in Debian we don't (we have to activate it).</h3>

<img src="pics/linux-firewall.png" width="800" />
<br>
<br>

<img src="pics/firewall-1.png" width="800" />
<br>
<br>

Firewalld is the high level user interface that we use to manage firewall configurations. Firewalld ahs 2 configurations:
1. Permanent configuration - stored in the filesystem
2. Active/Runtime configuration - stored in the memory

<img src="pics/common-firewall-cmd-commands.png" width="800" />
<br>
<br>

<img src="pics/common-firewall-cmd-commands-1.png" width="800" />
<br>
<br>

When we make changes over the firewall we need to choose where we make these changes - in the permanent config or in the active/runtime config. 
- If we make the changes in the active/runtime config, the changes are active in the current session but removed when we restart the system.
- If we make the changes in the permanent firewall config, the changes are not active in the current session but enabled after system or service restart.

Common approach is when we make changes in active/runtime firewall configs, we then save the changes into permanent configs and vice versa - if we make changes in the permanent firewall configs then we restart the system/service.

<img src="pics/firewall-2.png" width="800" />
<br>
<br>

UFW is high level user interface the we use to manage firewall configs in Debian. Here we have more simplistic structure - no zones, no active and permanent configs and services but applications.

<img src="pics/common-ufw-commands.png" width="800" />
<br>
<br>

<img src="pics/common-ufw-commands-1.png" width="800" />
<br>
<br>

### Secure Shell (SSH) Introduction 

<img src="pics/ssh.png" width="800" />
<br>
<br>

<img src="pics/ssh-1.png" width="800" />
<br>
<br>

### Dynamic Host Configuration Protocol Introduction

<img src="pics/dhcp.png" width="800" />
<br>
<br>

We can use reservations configs with DHCP when we configure servers. Static is when we set specific configurations for specific device/role (server) in the network - MAC/IP static configs. This mean that when configurations are distributed by DHCP the specific MAC will receive the same IP (and other configs) every time. This approach is used so we can easily reorganize our network except the reserved devices/roles.

<img src="pics/dhcp-1.png" width="800" />
<br>
<br>

<img src="pics/dhcp-2.png" width="800" />
<br>
<br>


### Practice

<h3>We will create small network with AlmaLinux</h3>

We can find the task descritpion in file M4-Practice-Networks-Software-Services-AlmaLinux.pdf in the resources.

<img src="pics/network-example-almalinux-task-3.png" width="800" />
<br>
<br>

Create 2 clones of already created machine in the beggining of the course and regenerate the MAC address fo the clones.

<img src="pics/alma-create-clone-machine.png" width="800" />
<br>
<br>

<img src="pics/alma-create-clone-machine-1.png" width="800" />
<br>
<br>

Change the network settings of the clones

<img src="pics/alma-vms-change-network-configs.png" width="800" />
<br>
<br>

<img src="pics/alma-vms-change-network-configs-1.png" width="800" />
<br>
<br>

Start the VMs and rename first of them with the static IP address.

Login to station 1

    terminal --> user
    terminal --> user pass

Rename the station

    terminal --> sudo hostnamectl set-hostname venus.lsa.lab
    terminal --> user pass

Set pretty name

    terminal --> sudo hostnamectl set-hostname --pretty 'Venus station'

Exit and login angain in the station

    terminal --> exit

    terminal --> user
    terminal --> user pass

Check the names

    terminal --> hostnamectl

Configure the network config - set static IP address

    terminal --> ip a

    terminal --> sudo nmtui

<img src="pics/station-1-network-config-1.png" width="300" />
<br>
<br>

<img src="pics/station-1-network-config-2.png" width="300" />
<br>
<br>

<img src="pics/station-1-network-config-3.png" width="800" />
<br>
<br>

<img src="pics/station-1-network-config-4.png" width="300" />
<br>
<br>

Ping the server

    terminal --> ping 192.168.200.1

Login into the second VM that will get IP dynamically.

    terminal --> user
    terminal --> user@pass

Rename the VM and set pretty name as well

    terminal --> sudo hostnamectl set-hostname mars.lsa.lab
    terminal --> user@pass

Set pretty name

    terminal --> sudo hostnamectl set-hostname --pretty 'Mars station'

Exit and login angain in the station

    terminal --> exit

    terminal --> user
    terminal --> user@pass

Check the names

    terminal --> hostnamectl

Login into the server again with SSH

    terminal --> ssh -p 10002 user@localhost
    terminal --> user@pass

Install DHCP on the server

    terminal --> sudo dnf install -y kea
    terminal --> user@pass

Open for edit DHCP config file

    terminal --> sudo vi /etc/kea/kea-dhcp4.conf

- delete all lines
  
    terminal --> 500dd

- paste the conigs below

```json
{
"Dhcp4": {
    "interfaces-config": {
        "interfaces": [ "enp0s8" ]
    },
    "expired-leases-processing": {
        "reclaim-timer-wait-time": 10,
        "flush-reclaimed-timer-wait-time": 25,
        "hold-reclaimed-time": 3600,
        "max-reclaim-leases": 100,
        "max-reclaim-time": 250,
        "unwarned-reclaim-cycles": 5
    },
    "renew-timer": 900,
    "rebind-timer": 1800,
    "valid-lifetime": 3600,
    "option-data": [
    {
        "name": "domain-name-servers",
        "data": "8.8.8.8"
    },
    {
        "name": "domain-name",
        "data": "lsa.lab"
    },
    {
        "name": "domain-search",
        "data": "lsa.lab"
    }
],
"subnet4": [
    {
        "id": 1,
        "subnet": "192.168.200.0/24",
        "pools": [ { "pool": "192.168.200.100 - 192.168.200.120" } ],
        "option-data": [
            {
                "name": "routers",
                "data": "192.168.200.1"
            }
        ]
    }
],
"loggers": [
{
    "name": "kea-dhcp4",
    "output-options": [
        {
            "output": "/var/log/kea/kea-dhcp4.log"
        }
    ],
    "severity": "INFO",
    "debuglevel": 0
  }
 ]
}
}
```

- save the file and exit

    terminal --> :wq!

Test the configuration

    terminal --> sudo kea-dhcp4 -t /etc/kea/kea-dhcp4.conf
    terminal --> user@pass

    # result: warnings and info (WARN, INFO) but no errors should appear
    2026-04-15 20:22:49.152 WARN  [kea-dhcp4.dhcpsrv/1089.140606965094528] DHCPSRV_MT_DISABLED_QUEUE_CONTROL disabling dhcp queue control when multi-threading is enabled.
    2026-04-15 20:22:49.153 WARN  [kea-dhcp4.dhcp4/1089.140606965094528] DHCP4_RESERVATIONS_LOOKUP_FIRST_ENABLED Multi-threading is enabled and host reservations lookup is always performed first.
    2026-04-15 20:22:49.154 INFO  [kea-dhcp4.dhcpsrv/1089.140606965094528] DHCPSRV_CFGMGR_NEW_SUBNET4 a new subnet has been added to configuration: 192.168.200.0/24 with params: t1=900, t2=1800, valid-lifetime=3600
    2026-04-15 20:22:49.154 INFO  [kea-dhcp4.dhcpsrv/1089.140606965094528] DHCPSRV_CFGMGR_SOCKET_TYPE_SELECT using socket type raw
    2026-04-15 20:22:49.156 INFO  [kea-dhcp4.dhcpsrv/1089.140606965094528] DHCPSRV_CFGMGR_ADD_IFACE listening on interface enp0s8
    2026-04-15 20:22:49.156 INFO  [kea-dhcp4.dhcpsrv/1089.140606965094528] DHCPSRV_CFGMGR_SOCKET_TYPE_DEFAULT "dhcp-socket-type" not specified , using default socket type raw
    2026-04-15 20:22:49.156 INFO  [kea-dhcp4.dhcpsrv/1089.140606965094528] DHCPSRV_LEASE_MGR_BACKENDS_REGISTERED the following lease backend types are available: memfile
    2026-04-15 20:22:49.156 INFO  [kea-dhcp4.hosts/1089.140606965094528] HOSTS_BACKENDS_REGISTERED the following host backend types are available:
    2026-04-15 20:22:49.156 INFO  [kea-dhcp4.dhcpsrv/1089.140606965094528] DHCPSRV_FORENSIC_BACKENDS_REGISTERED the following forensic backend types are available:
    2026-04-15 20:22:49.156 INFO  [kea-dhcp4.database/1089.140606965094528] CONFIG_BACKENDS_REGISTERED the following config backend types are available:

Start the DHCP service

    terminal --> sudo systemctl start kea-dhcp4

Set to start automatically in system start

    terminal --> sudo systemctl enable kea-dhcp4

    # result: Created symlink '/etc/systemd/system/multi-user.target.wants/kea-dhcp4.service' → '/usr/lib/systemd/system/kea-dhcp4.service'.

Check the status of the service

    terminal --> systemctl status kea-dhcp4

    # result:
    ● kea-dhcp4.service - Kea DHCPv4 Server
        Loaded: loaded (/usr/lib/systemd/system/kea-dhcp4.service; enabled; preset: disabled)
        Active: active (running) since Wed 2026-04-15 20:24:26 CEST; 1min 31s ago
    Invocation: 715632c51ae9475b9e11f161eac2d663
        Docs: man:kea-dhcp4(8)
    Main PID: 1100 (kea-dhcp4)
        Status: "Dispatching packets..."
        Tasks: 6 (limit: 12288)
        Memory: 2.4M (peak: 6.2M)
            CPU: 36ms
        CGroup: /system.slice/kea-dhcp4.service
                └─1100 /usr/sbin/kea-dhcp4 -c /etc/kea/kea-dhcp4.conf

Login into the VM that will get dynamically IP address (Mars) and check for IP settings

    terminal --> ip a

    # result: we should not see assigned IP address yet.

Force turn off and turn on the network adapter enp0s3

    terminal --> sudo nmcli conn down enp0s3 ; sudo nmcli conn up enp0s3
    terminal --> user@pass

After the restart we can list the IP configs and see that the network adapter has automatically assigned IP address 192.168.200.100

    terminal --> ip a

The connection with the server should be established

    terminal --> ping 192.168.200.1

Try to ping the Venus VM (machine with static IP 192.168.200.2). THe connection also should be established successful.

    terminal --> ping 192.168.200.2

Try to ping the external DNS - 8.8.8.8. The connection should be failing because we haven't configure the server for external (internet access) yet.

    terminal --> ping 8.8.8.8

Exit Mars station

    terminal --> exit


Go to the server VM (jupiter) and check if the firewall is enabled

    terminal --> systemctl status firewalld

    # result:
    ● firewalld.service - firewalld - dynamic firewall daemon
        Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; preset: enabled)
        Active: active (running) since Wed 2026-04-15 20:02:59 CEST; 43min ago
    Invocation: 50062c75d78b4414946263610a55961d
        Docs: man:firewalld(1)
    Main PID: 774 (firewalld)
        Tasks: 2 (limit: 12288)
        Memory: 49M (peak: 70.3M)
            CPU: 1.190s
        CGroup: /system.slice/firewalld.service
                └─774 /usr/bin/python3 -sP /usr/sbin/firewalld --nofork --nopid

    Apr 15 20:02:56 jupiter.sla.lab systemd[1]: Starting firewalld.service - firewalld - dynamic firewall daemon...
    Apr 15 20:02:59 jupiter.sla.lab systemd[1]: Started firewalld.service - firewalld - dynamic firewall daemon.

Check the zones of the firewall

    terminal --> sudo firewall-cmd --get-active-zones
    terminal --> user@pass

    # result:
    public (default)
      interfaces: enp0s3 enp0s8

We need to place these network interfaces in different zones. 

First we place the external network adapter to 'external' zone

    terminal --> sudo nmcli connection modify enp0s3 connection.zone external

Then we plcae the internal network adapter itno 'trusted' zone

    terminal --> sudo nmcli connection modify enp0s8 connection.zone trusted

Check zone again 

    terminal --> sudo firewall-cmd --get-active-zones
    terminal --> user@pass

    # result:
    external
      interfaces: enp0s3
    trusted
      interfaces: enp0s8
    public (default)

Enable check and enable the NAT functionality if not enabled already

    terminal --> sudo firewall-cmd --zone=external --add-masquerade --permanent

    terminal --> sudo firewall-cmd --reload

This zone configs enables automatically IP forwarding. This allows our server to foreward traffic in and out of our internal netwrok where aour other VMs are connected (play as router). Check the settings:

    terminal --> cat /proc/sys/net/ipv4/ip_forward

    # result: 1

We can now connect to the other VMs from the server.

Connect to Venus (static IP VM)

    terminal --> ssh 192.168.200.2
    terminal --> yes
    terminal --> user@pass

In Venus VM we can now ping the google DNS we configured - 8.8.8.8. The connection should be successful. Then exit the Venus VM

    venus terminal --> ping 8.8.8.8
    venus terminal --> exit

Login into Mars (VM with dynamically IP configuration).

    terminal --> ssh 192.168.200.100
    terminal --> yes
    terminal --> user@pass

In Mars VM ping google DNS - 8.8.8.8. The connection should be successful.

    mars terminal --> ping 8.8.8.8


If we want to connect to Venus or Mars stations with theur names we need to add thir IPs and names in the server hosts list

    jupiter terminal --> sudo vi /etc/hosts

```yaml
# Loopback entries; do not change.
# For historical reasons, localhost precedes localhost.localdomain:
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
# See hosts(5) for proper format and other examples:
# 192.168.1.10 foo.example.org foo
# 192.168.1.13 bar.example.org bar

192.168.200.1   jupiter.sla.lab jupiter
192.168.200.2   venus.lsa.lab   venus
192.168.200.100 mars.lsa.lab    mars
```
save and exit the file      
    terminal --> :qw!

Now we can access Venus and Mars with their names. Ping them:

    jupiter terminal --> ping venus
    jupiter terminal --> ping mars

If we want to access and ping VMs from the venus or Mars we need to set the same records on them also (/etc/hosts).

Connections to different VMs are made with specific port and user if they are configured different from the default ones. 


Also we can connect true SSH with key pairs.

Generate ssh keys on the server

    jupiter terminal --> ssh-keygen

Show the keys on the server

    terminal --> ls -al ~/.ssh

    # result:
    total 16
    drwx------. 2 user user   88 Apr 15 22:09 .
    drwx------. 3 user user  111 Apr 15 21:50 ..
    -rw-------. 1 user user  411 Apr 15 22:09 id_ed25519            # private key
    -rw-r--r--. 1 user user  102 Apr 15 22:09 id_ed25519.pub        # public key
    -rw-------. 1 user user 1680 Apr 15 21:08 known_hosts
    -rw-------. 1 user user  934 Apr 15 21:08 known_hosts.old

Copy the public key to Venus - we must confirm the user and password to set the key for it.

    terminal --> ssh-copy-id venus
    terminal --> yes
    terminal --> user@pass

    # result:
    /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/user/.ssh/id_ed25519.pub"
    The authenticity of host 'venus (192.168.200.2)' can't be established.
    ED25519 key fingerprint is SHA256:d1Wxljwhk2O0I7hCl7Kchkg73vYRZ5/MMULIg3cAbA0.
    This host key is known by the following other names/addresses:
        ~/.ssh/known_hosts:1: 192.168.200.2
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
    /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
    user@venus's password:

    Number of key(s) added: 1

    Now try logging into the machine, with: "ssh 'venus'"
    and check to make sure that only the key(s) you wanted were added.


Copy the public key to Mars - we must confirm the user and password to set the key for it.

    terminal --> ssh-copy-id mars
    terminal --> yes
    terminal --> user@pass

    # result:
    /usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/user/.ssh/id_ed25519.pub"
    The authenticity of host 'mars (192.168.200.100)' can't be established.
    ED25519 key fingerprint is SHA256:2M6XHAGTJMy2WIbJu0k9SG4pwtRiCkpEwjQWOaSnb5E.
    This host key is known by the following other names/addresses:
        ~/.ssh/known_hosts:4: 192.168.200.100
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    /usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
    /usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
    user@mars's password:

    Number of key(s) added: 1

    Now try logging into the machine, with: "ssh 'mars'"
    and check to make sure that only the key(s) you wanted were added.

Now we can connect to venus or mars without password

    terminal --> ssh venus
    or
    terminal --> ssh mars

Good practice is to create pair keys and copu the public key to the target machine. In production the pair keys are protected with password!!!
- more appropriate - no passwords
- more secure

[⬆ Back to top](#top)