# Section 4 Working on the Console. Users and Access Management

Content

- [Section 4 Working on the Console. Users and Access Management](#section-4-working-on-the-console-users-and-access-management)
  - [Console Deep Dive](#console-deep-dive)
  - [Command Execution - Executable Artifacts. Order of Execution](#command-execution---executable-artifacts-order-of-execution)
  - [Practice](#practice)
  - [Working with Files](#working-with-files)
  - [Users and Groups](#users-and-groups)
    - [Access Rights](#access-rights)


<p style="font-size:16px;"><strong>Important text</strong></p>
<h3>Important text</h3>
<img src="pics/name.png" width="800" />
<br>
<br>

## Console Deep Dive

[⬆ Back to top](#top)

- General purpose   
  - $? => Return the exit code of last executed command   
  - $! => Return the PID of the last job run in background    
  - '$$' => Return the PID of the current process   
  - $_ => Return the final argument of the previous command   

- Prompt related    
  - $PS1 => Regular prompt    
  - $PS2 => Prompt during multi-line commands   


Code                Display   
\h       ->         Hostname until the first '.'    
\H       ->         Full hostname   
\t       ->         Current time in 24-hour format HH:MM:SS   
\A       ->         Current time in 24-hour format HH:MM    
\u       ->         Username of the current user    
\w       ->         Current working directory   
\W       ->         Base name of the current working directory    
\#       ->         Command number of this command    
\$       ->         If UID=0 then it is '#' otherwise it is '$    

set
- Purpose
  - Controls shell options. Display values of shell variables
- Syntax
  - bash --> set [options] [+/-o shell options] [arguments]
  
- Examples
Display shell options suitable for re-use
[user@host ~]$ set +o
Display all shell variable names and values
[user@host ~]$ set


unset
- Purpose
  - Unset values and attributes of shell variables and functions
- Syntax
  - bash --> unset [options] [name]

- Examples
Unset single variable
[user@host ~]$ unset MYVAR1
Unset multiple variables
[user@host ~]$ unset -v MYVAR1 MYVAR2 MYVAR3

[⬆ Back to top](#top)

## Command Execution - Executable Artifacts. Order of Execution

[⬆ Back to top](#top)

External Commands - Scripts, Binary Files

Special Types - Aliases, Functions

<h3>Command Execution (Shell's Perspective)</h3>

<img src="pics/shell-exec.png" width="800" />
<br>
<br>

<h3>Scripts</h3>

We have 2 ways of script execution

- Sourcing
  - No subshell is created
  - Any variables set become part of the environment
  - Methods: <strong>. script.sh</strong> or <strong>source script.sh</strong>

- Execution
  - Subshell is always created (except for the built-in commands)
  - No subshell if using <strong>exec ./script.sh</strong>


<h3>Execution (Search) Order</h3>

<img src="pics/execution-order.png" width="800" />
<br>
<br>

<h3>Break the Order</h3>

- Force Built-in Usage
  - [user@host ~]$ builtin test
- Set Explicit Path
  - [user@host ~]$ /bin/test
- Ignore Aliases and Functions
  - [user@host ~]$ command test
- Ignore Just Aliases
  - [user@host ~]$ \test


<h3>hash</h3>

- Purpose
  - Remembers or display program locations
- Syntax
  - hash [options] [name]
- Examples
  - Display re-usable list of program locations   
    - [user@host ~]$ hash -l
  - Add a program location to the list    
    - [user@host ~]$ hash -p /bin/ping ping


<h3>whereis</h3>

- Purpose
  - Locates the binary, source, and man page files for a command
- Syntax
  - whereis [options] name [name …]
- Examples
  - Display all files for a command
    - [user@host ~]$ whereis ls
  - Display only binary file information
    - [user@host ~]$ whereis -b ls


<h3>which</h3>

- Purpose
  - Shows the full path of (shell) commands
- Syntax
  - which [options] name [name …]
- Examples
  - Show what would have been executed
    - [user@host ~]$ which cd
  - Print all matching executables in PATH
    - [user@host ~]$ which -a cd

<h3>type</h3>

- Purpose
  - Displays information about command type
- Syntax
  - type [options] name [name …]
- Examples
  - Show everything about a single command
    - [user@host ~]$ type -a ls
  - Print information about multiple commands
    - [user@host ~]$ type cd ls pwd

<h3>alias</h3>

- Purpose
  - Define or display aliases
- Syntax
  - alias [-p] [name[=value]]
- Examples
  - Print all aliases in re-usable format
    - [user@host ~]$ alias -p
  - Define new alias
    - [user@host ~]$ alias si='uname -a'

<h3>unalias</h3>

- Purpose
  - Removes alias
- Syntax
  - unalias [-a] name [name …]
- Examples
  - Remove all aliases
    - [user@host ~]$ unalias -a
  - Remove two aliases
    - [user@host ~]$ unalias ls ll

<h3>export</h3>

- Description
  - Sets export attribute for shell variables - when we export a variable, the env become usable in all subsessions 
  
- Example

<img src="pics/export-example.png" width="800" />
<br>
<br>


<h3>env</h3>

- Description
  - Runs a program in a modified environment
- Example

<img src="pics/env-example.png" width="800" />
<br>
<br>

---

<h3>Configuration Files</h3> What Drives the BASH Shell?  

---  

<strong>System Level Configuration</strong>

- Stored in <strong>/etc</strong>
- File profile
  - Used for <strong>Environment</strong> control and <strong>Startup</strong> programs execution
- File <strong>bashrc</strong> (Red Hat) or <strong>bash.bashrc</strong> (Debian, openSUSE)
  - Used for <strong>Functions</strong> and <strong>Aliases</strong> definition
- Folder <strong>profile.d/*</strong>
  - Used for custom routines definition
  - It is read by <strong>profile</strong> (all), <strong>bashrc</strong> (Red Hat), and <strong>bash.bashrc</strong> (openSUSE)    


<strong>User Level Configuration</strong>

- Stored in <strong>user's home directory</strong>
- File <strong>.bash_profile</strong> (Red Hat) or <strong>.profile</strong> (Debian, openSUSE)
  - Executed only in <strong>login shell</strong>
  - Reads <strong>~/.bashrc</strong>
- File <strong>.bashrc</strong> (all)
  - Executed <strong>always</strong>
  - Reads <strong>/etc/bashrc</strong> (Red Hat)    
<br>
<br>

<strong>Login Shell Sequence (Red Hat)</strong>

<img src="pics/login-sequence.png" width="600" />
<br>
<br>

<strong>Non-login Shell Sequence (Red Hat)</strong>

<img src="pics/non-login-sequence.png" width="600" />
<br>
<br>

[⬆ Back to top](#top)

## Practice

[⬆ Back to top](#top)

Create VM with AlmaLinux with instructions from section 3 Introduction to Linux - [Manage AlmaLinux VM](../3.%20Introduction%20to%20Linux/Section%203%20Introduction%20to%20Linux%20Notes.md#manage-almalinux-vm)

<strong>Set AlmaLinux VM port forwarding</strong>

<img src="pics/alma-port-forwarding.png" width="800" />
<br>
<br>


<strong>Start the AlmaLinux VM and connect via SSH</strong>

<img src="pics/almalinux-start.png" width="800" />
<br>
<br>

    bash -->  ssh -p 10002 user@localhost
    bash --> yes
    bash --> user password

<img src="pics/ssh-almalinux.png" width="800" />
<br>
<br>

<h3>Is it possible to receive a caution message with duplicated remote hosts (different VM template or linux distro), we need to delete them in the host list.</h3>

<img src="pics/alma-login-caution-1.png" width="800" />
<br>
<br>

<img src="pics/alma-login-caution-2.png" width="800" />
<br>
<br>

<strong>list PATH</strong>

    [user@almalinux ~]$ echo $PATH

    # result: 
    /home/user/.local/bin:/home/user/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin

<strong>Find command location</strong>

    [user@almalinux ~]$ whereis ls

    # result:
    ls: /usr/bin/ls /usr/share/man/man1/ls.1.gz

<strong>Find command function</strong>

    [user@almalinux ~]$ whatis ls

    # result:    ls: nothing appropriate.

<strong>Find command type</strong>

    [user@almalinux ~]$ type ls

    # result:
    ls is aliased to `ls --color=auto'

<strong>Manage variables</strong>

- Create variable

    bash --> MYVAR=Demo

- Print variable

    bash --> echo $MYVAR

    result: Demo

- Make variable avalable to all subsessions

    bash --> export MYVAR2=Child

- Start subsession

  bash --> bash

  - print the first variable
  
    bash --> echo $MYVAR

    result: 

  - print exported variable

    bash --> echo $MYVAR2

    result: Child

- Print the level of the sessions we are in

    bash --> echo $SHLVL

    result: 2

- Exit the subsession and check the level again

    bash --> exit

    bash --> echo $SHLVL

    result: 1

<strong>When we change variable in subsession, the change is not made in the parent session !!!</strong> 


<h3>Hash</h3>

<strong>List executed commands</strong>

    bash --> hash

    # result:
    hits    command
      3    /usr/bin/whatis
      4    /usr/bin/bash
      1    /usr/bin/whereis

<h3>List aliases</h3>

    bash --> alias

    # result:
    alias egrep='grep -E --color=auto'
    alias fgrep='grep -F --color=auto'
    alias grep='grep --color=auto'
    alias l.='ls -d .* --color=auto'
    alias ll='ls -l --color=auto'
    alias ls='ls --color=auto'
    alias which='(alias; declare -f) | /usr/bin/which --tty-only --read-alias --read-functions --show-tilde --show-dot'
    alias xzegrep='xzegrep --color=auto'
    alias xzfgrep='xzfgrep --color=auto'
    alias xzgrep='xzgrep --color=auto'
    alias zegrep='zegrep --color=auto'
    alias zfgrep='zfgrep --color=auto'
    alias zgrep='zgrep --color=auto'


[⬆ Back to top](#top)


## Working with Files

Explore, Know, and Rule Those Files

[⬆ Back to top](#top)

<strong>Everything is Files</strong>

- Naming conventions
  - Case sensitive (file.txt <> File.txt <> FILE.TXT)
  - Stick to alphanumeric characters
  - Substitute spaces with (_ , - , .)
  - Extensions are not needed, but nice to have

- Work with multiple files
  - Helper symbols when reading or listing (*, ? , [] , {})
  - Techniques when creating ({X,Y,Z}, {A..D}, {1..10})

<img src="pics/file-types.png" width="600" />
<br>
<br>

<h3>file</h3>

- Purpose
  - Determine file type
- Syntax
  - file [options] file [file …]
- Examples
  - Show information about a file    
    - [user@host ~]$ file /etc/profile
  - Show information about multiple files      
    - [user@host ~]$ file /etc/*.conf


<h3>stat</h3>

- Purpose
  - Display file or file system status    
- Syntax
  - stat [options] file [file …]    
- Examples
  - Show information about a file       
    - [user@host ~]$ stat .bash_history   
  - Show information about files in a special format       
    - [user@host ~]$ stat --terse /etc/*.conf


<h3>touch</h3>

- Purpose
  - Change file timestamp      
- Syntax
  - touch [options] file [file …]      
- Examples
  - Change access time of a file           
    - [user@host ~]$ touch -a .bash_history   
  - Create an empty file      
    - [user@host ~]$ touch emptyfile.txt    


<h3>cp</h3>

- Purpose
  - Copy files and directories         
- Syntax
  - cp [options] source dest         
- Examples
  - Copy single file               
    - [user@host ~]$ cp file1.txt ~/Documents/my-file.txt     
  - Copy multiple files to a folder      
    - [user@host ~]$ cp /etc/*.conf ~/Temp/    


<h3>mv</h3>

- Purpose
  - Move (rename) files         
- Syntax
  - mv [options] source dest            
- Examples    
  - Rename a file                  
    - [user@host ~]$ mv fileA.txt fileB.txt       
  - Move multiple files to a folder        
    - [user@host ~]$ mv *.bak ~/Backup/    


<h3>rm</h3>

- Purpose
  - Remove files or directories          
- Syntax
  - rm [options] file [file …]               
- Examples    
  - Remove multiple files                   
    - [user@host ~]$ rm file?.txt         
  - Remove folder and its contents           
    - [user@host ~]$ rm -rf ~/Temp      


<h3>mkdir</h3>

- Purpose
  - Make directories             
- Syntax
  - mkdir [options] directory [directory …]                 
- Examples    
  - Create two directories                       
    - [user@host ~]$ mkdir dir1 dir2            
  - Create nested directories               
    - [user@host ~]$ mkdir -pv projects/project{1..5}   


<h3>rmdir</h3>

- Purpose
  - Remove empty directories          
- Syntax
  - rmdir [options] directory [directory …]                 
- Examples    
  - Remove two empty directories                     
    - [user@host ~]$ rmdir dir1 dir2            
  - Remove directory and its ancestors               
    - [user@host ~]$ rmdir -pv projects/project1/phaseA      


<h3>ln - link</h3>

- Purpose
  - Make links between files         
- Syntax
  - ln [options] target link_name (1st form)              
- Examples    
  - Create a hard link - create alias to an object. To delete an object we need to delete all aliases.             
    - [user@host ~]$ ln file.txt ~/Documents/fileH.txt           
  - Create a soft link - create shortcut to object. We can delete the shortcut, but the object still exist. If we delete the object the soft link still exist but is broken.              
    - [user@host ~]$ ln -s file.txt ~/Documents/fileS.txt     


<h3>Absolute vs Relative Path</h3>

- Absolute Path (starts with /)   
  - Calculated from the root of the file system tree    
- Relative Path (no leading /)    
  - Calculated from the current working directory   
- If we are in /home/user and we want to create /shared/temp    
  - Absolute notation   
    - [user@host ~]$ sudo mkdir -p /shared/temp   
  - Relative notation   
    - [user@host ~]$ sudo mkdir -p ../../shared/temp    


<strong>Practice in video from 3:00h to 3:20h</strong>
- Create folders - tree
- Move and delete folders - filter folders
- Relative and absolute path management

[⬆ Back to top](#top)

## Users and Groups

Manage Users and Groups

[⬆ Back to top](#top)

<img src="pics/user-main-file.png" width="800" />
<br>
<br>

<img src="pics/user-password-file.png" width="800" />
<br>
<br>

<img src="pics/user-defaults-during-creation.png" width="800" />
<br>
<br

<img src="pics/groups-main-file.png" width="800" />
<br>
<br>

<img src="pics/groups-password-file.png" width="800" />
<br>
<br>


<h3>useradd</h3>

- Purpose
  - Create a new user or update default new user information           
- Syntax
  - useradd [options] login               
- Examples    
  - Create new user               
    - [user@host ~]$ sudo useradd newuser         
  - Set a default expiry date              
    - [user@host ~]$ sudo useradd -D -e 2019-12-31   

<h3>usermod</h3>

- Purpose
  - Modify a user account          
- Syntax
  - usermod [options] login           
- Examples    
  - Change user's full name (comment field)               
    - [user@host ~]$ sudo usermod -c 'Demo' newuser           
  - Add user to a group                 
    - [user@host ~]$ sudo usermod -aG demogroup newuser


<h3>userdel</h3>

- Purpose
  - Delete a user account and related files             
- Syntax
  - userdel [options] login           
- Examples    
  - Remove a user without removing its home folder                   
    - [user@host ~]$ sudo userdel newuser             
  - Remove a user and its home folder                 
    - [user@host ~]$ sudo userdel -r newuser    



<h3>adduser (Debian)</h3>

- Purpose
  - Create a new user (regular or system)*         
- Syntax
  - adduser [options] user           
- Examples    
  - Create new user               
    - [user@host ~]$ sudo adduser helpdesk             
  - Add an existing user to an existing group                 
    - [user@host ~]$ sudo adduser helpdesk itstaff



<h3>deluser (Debian)</h3>

- Purpose
  - Remove user (regular or system)*         
- Syntax
  - deluser [options] user              
- Examples    
  - Remove user                 
    - [user@host ~]$ sudo deluser helpdesk                
  - Remove user from a group                 
    - [user@host ~]$ sudo deluser helpdesk itstaff    



<h3>users</h3>

- Purpose
  - Print the usernames of users currently logged in           
- Syntax
  - users [options] [file]          
- Examples    
  - Print currently logged users               
    - [user@host ~]$ users                


<h3>w</h3>

- Purpose
  - Show who is logged on and what they are doing             
- Syntax
  - w [options] user         
- Examples    
  - Print information about the logged on users              
    - [user@host ~]$ w                
  - Print shorter version                  
    - [user@host ~]$ w --short


<h3>who</h3>

- Purpose
  - Show who is logged on           
- Syntax
  - who [options] [file | arg1 arg2]              
- Examples    
  - Print currently logged users with headers               
    - [user@host ~]$ who -Hu   


<h3>whoami</h3>

- Purpose
  - Print effective userid              
- Syntax
  - whoami [options]             
- Examples    
  - Print the effective user               
    - [user@host ~]$ whoami  


<h3>last</h3>

- Purpose
  - Show listing of last logged in users                
- Syntax
  - last [options]            
- Examples    
  - List the last five lines                 
    - [user@host ~]$ last -n 5                
  - Print full login and logout times and dates                    
    - [user@host ~]$ last -F


<h3>lastb</h3>

- Purpose
  - Show listing of last unsuccessful login attempts                
- Syntax
  - lastb [options]           
- Examples    
  - List the last five lines                 
    - [user@host ~]$ sudo lastb -n 5               
  - Display full user and domain names                    
    - [user@host ~]$ sudo lastb -w


<h3>lastlog</h3>

- Purpose
  - Report most recent login for all users                 
- Syntax
  - lastlog [options]            
- Examples    
  - List users and the last time they logged in               
    - [user@host ~]$ lastlog  


<h3>passwd</h3>

- Purpose
  - Update user's authentication tokens               
- Syntax
  - passwd [options] [login]             
- Examples    
  - Change password for the logged user                   
    - [user@host ~]$ passwd                 
  - Change password for another user                    
    - [user@host ~]$ sudo passwd username   



<h3>chpasswd</h3>

- Purpose
  - Update passwords in batch mode                    
- Syntax
  - chpasswd [options]                
- Examples    
  - Change password for a user                 
    - [user@host ~]$ echo username:password | sudo chpasswd  


<h3>chage*</h3>

- Purpose   
  - Change user password expiry information               
- Syntax    
  - chage [options] login             
- Examples    
  - Show account aging information                  
    - [user@host ~]$ chage -l user                 
  - Set expiry date for an account                    
    - [user@host ~]$ sudo chage -E 2019-12-31 username     


<h3>chfn*</h3>

- Purpose   
  - Change user finger (descriptive) information               
- Syntax    
  - chfn [options] [login]             
- Examples    
  - Change finger information for the current user                     
    - [user@host ~]$ chfn                    
  - Set full name and office of a user                    
    - [user@host ~]$ sudo chfn -f 'User 2' -o 'IT' user2 


<h3>chsh*</h3>

- Purpose   
  - Change user shell               
- Syntax    
  - chsh [options] [login]              
- Examples    
  - List available shells                     
    - [user@host ~]$ chsh --list-shells                    
  - Change the shell of a user                    
    - [user@host ~]$ sudo chsh -s /bin/sh user2


<h3>groupadd</h3>

- Purpose   
  - Create a new group               
- Syntax    
  - groupadd [options] group              
- Examples    
  - Add group and assign the next available id                     
    - [user@host ~]$ sudo groupadd accounting                    
  - Add group with custom id                    
    - [user@host ~]$ sudo groupadd -g 2000 developers


<h3>groupmod</h3>

- Purpose   
  - Modify a group definition on the system               
- Syntax    
  - groupmod [options] group              
- Examples    
  - Rename a group                      
    - [user@host ~]$ sudo groupmod -n newname oldname                    
  - Change group id                    
    - [user@host ~]$ sudo groupmod -g 1500 accounting


<h3>groupdel</h3>

- Purpose   
  - Delete a group               
- Syntax    
  - groupdel [options] group              
- Examples    
  - Delete a group                      
    - [user@host ~]$ sudo groupdel accounting                   


<h3>addgroup (Debian)</h3>

- Purpose   
  - Create a new user or system group*              
- Syntax    
  - addgroup [options] group              
- Examples    
  - Create new user group                      
    - [user@host ~]$ sudo addgroup itstaff                   
  - Create new system group                    
    - [user@host ~]$ sudo addgroup --system daemons


<h3>delgroup (Debian)</h3>

- Purpose   
  - Remove user or system groups*                 
- Syntax    
  - delgroup [options] group              
- Examples    
  - Remove user group                         
    - [user@host ~]$ sudo delgroup itstaff                   
  - Remove system group                    
    - [user@host ~]$ sudo delgroup --system daemons


<h3>groups</h3>

- Purpose   
  - Print the groups a user is in                 
- Syntax    
  - groups [options] [username]              
- Examples    
  - Print list of groups to which a user belongs                         
    - [user@host ~]$ groups                  


<h3>gpasswd</h3>

- Purpose   
  - Administer groups and their passwords                 
- Syntax    
  - gpasswd [options] group              
- Examples    
  - Change password of a group                         
    - [user@host ~]$ sudo gpasswd developers                  
  - Set a user as administrator for a group                    
    - [user@host ~]$ sudo gpasswd -A user developers


<h3>newgrp</h3>

- Purpose   
  - Log in to a new group - change current group for the session (change main group)                 
- Syntax    
  - newgrp [-] [group]               
- Examples    
  - Change current group                         
    - [user@host ~]$ newgrp developers                  
  - Simulates user login while changing the group                    
    - [user@host ~]$ newgrp - developers


<h3>id</h3>

- Purpose   
  - Print real and effective user and group IDs                 
- Syntax    
  - id [option] [user]              
- Examples    
  - Print user and group information for current user                        
    - [user@host ~]$ id                  
  - Print group IDs of a user                    
    - [user@host ~]$ id -G newuser


<h3>sudo</h3>

- Purpose   
  - Execute a command as another user                 
- Syntax    
  - sudo [options]             
- Examples    
  - Execute command as root                        
    - [user@host ~]$ sudo useradd testuser                  
  - Execute command as another user                    
    - [user@host ~]$ sudo -u helpdesk ls /home/helpdesk


<h3>su</h3>

- Purpose   
  - Run a command with substitute user and group ID                 
- Syntax    
  - su [options] [-] [user]             
- Examples    
  - Switch to a user                        
    - [user@host ~]$ su helpdesk                 
  - Switch to a user with login shell                    
    - [user@host ~]$ su - helpdesk


### Access Rights

- Two levels
  - Level 1: Discretionary Access Control (DAC)
    - Regular file access permissions *
    - Access Control Lists (ACL) **
  - Level 2: Mandatory Access Control (MAC)
    - Typical examples - SELinux and AppArmor
- Applied from Level 1 to Level 2

- Current process UID and GID are compared with the UID and GID of the file being accessed with regards to the permissions set
- ACL is a list of permissions attached to an object in the file system. It extends standard permissions and allows more options

<img src="pics/access-rights.png" width="800" />
<br>
<br>

<img src="pics/access-rights-meaning.png" width="800" />
<br>
<br>

<img src="pics/access-rights-meaning-2.png" width="800" />
<br>
<br>

<img src="pics/access-rights-symbolic-notations.png" width="800" />
<br>
<br>

<img src="pics/access-rights-octal-notation.png" width="800" />
<br>
<br>

<img src="pics/access-rights-notations-side-by-side.png" width="800" />
<br>
<br>

<img src="pics/default-access-rights.png" width="800" />
<br>
<br>

<strong>Special Permissions – Sticky Bit</strong>

- Prevent non-owners of a file to delete it
- Usually used for directories
- Numeric permission is 1xxx
- Can be set in both ways

- Set sticky bit of a folder with permissions 755
  - [root@host ~]# chmod 1755 /dir
- Set sticky bit using a symbolic notation
  - [root@host ~]# chmod o+t /dir


<strong>Special Permissions – Set Group ID (SGID)</strong>

- Allows users to run a program as if it was member of the group
- Usually used for directories
- All new files are owned by the group
- Numeric permission is 2xxx
- Can be set in both ways

- Set SGID to a file with permissions 644
  - [root@host ~]# chmod 2644 script.sh
- Set SGID using a symbolic notation
  - [root@host ~]# chmod g+s script.sh


<strong>Special Permissions – Set User ID (SUID)</strong>

- Allows users to run a program as if it was its owner
- Usually, the owner is root
- Numeric permission is 4xxx
- Can be set in both ways

- Set SUID to a file with permissions 644
  - [root@host ~]# chmod 4644 script.sh
- Set SUID using a symbolic notation
  - [root@host ~]# chmod u+s script.sh



<h3>chmod</h3>

- Purpose   
  - Change file mode bits                 
- Syntax    
  - chmod [options] file             
- Examples    
  - Set fixed permissions*                        
    - [user@host ~]$ chmod 755 hello.sh                 
  - Remove execute permission for the group*                    
    - [user@host ~]$ chmod g-x hello.sh


<h3>chown</h3>

- Purpose   
  - Change file owner and group                 
- Syntax    
  - chown [options] [owner][:[group]] file        # ':' can be replaced by '.'             
- Examples    
  - Change both owner and group of a file*                        
    - [user@host ~]$ chown user:users file.txt                 
  - Change recursively the group for a folder*                    
    - [user@host ~]$ chown -R :developers project/


<h3>chgrp</h3>

- Purpose   
  - Change group ownership                 
- Syntax    
  - chgrp [options] group file                 
- Examples    
  - Change the group of a files*                        
    - [user@host ~]$ chgrp developers code*                 
  - Change recursively the group for a folder*                    
    - [user@host ~]$ chgrp -vR developers project/  


<h3>umask</h3>

- Purpose   
  - Display or set file mode mask                 
- Syntax    
  - umask [options] [mode]                  
- Examples    
  - Show current mask using the symbolic notation                        
    - [user@host ~]$ umask -S                 
  - Set new mask                    
    - [user@host ~]$ umask 0022  


<img src="pics/problem-add-user.png" width="800" />
<br>
<br>

<img src="pics/solution-add-user.png" width="800" />
<br>
<br>

[⬆ Back to top](#top)
