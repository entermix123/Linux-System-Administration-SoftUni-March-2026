1. Set VMs - Section 3 Introduction to Linux
   
2. Set SSH configs - Section 4 Working on the Console
   1. recreate ssh key - terminal --> ssh-keygen -R "[localhost]:10002"
   2. start the machine and connect to it with SSH
      1. terminal --> ssh -p 10002 user@localhost
      2. terminal --> yes
      3. terminal --> password
   
3. Rename sptation and set pretty name
   1. terminal --> sudo hostnamectl set-hostname jupiter.sla.lab
   2. terminal --> sudo hostnamectl set-hostname --pretty 'Jupiter Server'
   - show changes
   4. terminal --> hostnamectl
   
4. Set permanent IP of the network adapter
   1. list network adapters
      1. terminal --> ip link show
   2. list IP configurations for every adapter
      1. terminal --> ip a
   3. list connection
      1. terminal --> nmcli connection show
   4. Add connection with specific IP address
      1. terminal --> sudo nmcli connection add type ethernet ifname enp0s8 con-name enp0s8
   5. Add specific
      1. terminal --> sudo nmcli connection modify enp0s8 ipv4.addresses 192.168.200.1/24 ipv4.method manual
   6. Restart the adapter
      1. terminal --> sudo nmcli connection down enp0s8; sudo nmcli connection up enp0s8
   
5. Confirm that the IP address configs are successful
   1. List the connections
      1. terminal --> nmcli connection show
   2. list IP addresses
      1. terminal --> ip a
   3. Ping the IP
      1. terminal --> ping 192.168.200.1

6. 