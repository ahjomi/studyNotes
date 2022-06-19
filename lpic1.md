## tty terminal
:star: **tty**
+ Virtual terminal (also called a "virtual console")
    + Ctrl + Alt + F1 ( Return to GUI from virtual terminal )
    + Ctrl + Alt + F2 reaches tty2
    + Ctrl + Alt + F3 reaches tty3
    + Ctrl + Alt + F4 reaches tty4
    + Ctrl + Alt + F5 reaches tty5

## Virtual Directory structure
+ **Virtual directory**\
> A single structure that combines all the installed storage devices into a 
merged directory
#### Filesystem hierarchy standard (FHS)
+ **/boot** - Boot loader files
+ **/etc** - Configuration files ( system & apps )
+ **/home** - User files
+ **/media** - Removable media
+ **/mnt** - Removable media ( older location)
+ **/opt** - Third-party apps
+ **/tmp** - Temporary files
+ **/usr** - Linux program data
+ **/var** - Variale data ( example: log files )
+ **/usr/bin** - Linux user program binaries
+ **/usr/sbin** - Linux admin program binaries
+ **/usr/local** - Local installation program data

## Command Line Basic
:star: **uname**\
> Prints out the name of the kernel
+ uname -r 
    + Relese option, but version info
+ uname -v
    + Version option, but build info
+ uname -a
    + Show's everything

:star: **bash**
+ bash --version
    + Prints out bash version

#### Built-in command & External command 
:star: **type**
> It will let you know if the command is built-in or external

:star: **which**
>Determining where a command is located ( **Absolute directory** )
External commands are programs that reside within the virtual directory structure
+ man -k(Keyword search) which | grep ^which | tee studyMe.txt
+ man -k whereis | grep ^whereis | tee -a(Append) studyMe.txt
+ man -k updatedb | grep ^updatedb | tee -a studyMe.txt

:star: **man** 
> Manual pages

:star: **info** 
> Info help system

:star: **help** 
> Built-in command help

:star: **history** 
> View a list of entered commands

:star: **!!** 
> Use previously entered commands

:star: **~/.bash_history** 
> Where used commands are stored

## Displaying Text Contents & Information
:star: **ls**
+ ls -F
    + Displays a symbol called a classification indicator behind certain types
    + / = Directory
    + '*' = Executable file
    + @ = symbolic link 
+ ls /etc/PASSWD 2> error.txt
+ ls -dl (DirName)
    + How to view directory file information
+ ls -R (DirName)
    + Viewing a directory tree
+ ls -hs [fileName | dirName]
#### WildCards
+ ls -d /etc/*
+ ls -d /etc/net* or | *net*
+ ls -d /etc/network?
    + **?** wildcard will match any characters in **ONE** character position
+ ls -d /etc/liba[ou]
+ ls -d /etc/lib?[oul]*
+ ls -d /etc/lib?[a-Z]*
    + **[]** wildcard One character position to specified characters

:star: **cat**
> The cat command is used for concatenating files together, but is also used to display files

:star: **head**
> The head command shows the **first 10** lines of a text file
+ head -n 2 /etc/passwd == head -2 /etc/passwd
    + Prints out only 2 lines

:star: **tail**
> The tail command shows the **last 10** lines of a text file
+ tail -n 4 /etc/passwd == tail -4 /etc/passwd
    + Prints last 4 lines
+ tail -f /var/log/secure
    + Show the last message of the log file and display any new messages as they come in

**Pager utility**
> Is a utility that allows you to view a text file one page at a time

:star: **more**
+ more /var/log/(anyLogFiles)

:star: **less**
+ less /var/log/(anyLogFiles)

:star: **wc**
> Shows the number of lines, words, and bytes in the text file
+ wc -l (fileName)
    + only displays the line count
+ wc -w (fileName)
    + only displays the word count
+ wc -c (fileName)
    + only displays the byte count

:star: **uniq**
> Only shows the uniqe lines ( sort a file first before running the command ) 
+ uniq - c (fileName)
    + Count the occurrence of each line
+ uniq - d (fileName)
+ uniq - D (fileNmae)

:star: **nl** 
> Gives each line a number\
( It's helpful when you get an error message stating a problem is on a particular line number in a file )

#### Hash
 + A fixed-length string of letters and numbers

:star: **md5**
+ md5sum (fileName)

:star: **sha###**
+ sha256sum (fileName)
+ sha512sum (fileName) 

## Manipulating & Searching Text content
:star: **sort**
>Sorting a text file
>>alphabetically\
numerically
+ sort -n (fileName)
    + sorts file numerically
+ sort (fileName) > (newFile)

:star: **paste**
>Pasting twi files together

:star: **split**
>How to split a file into multiple file

:star: **cut**
>Extracting certain fields from text file records
+ cut -d : -f7 /etc/passwd
+ cut -c1-10 /etc/passwd

:star: **tr**
>Change a letter or number in text file to a different one
+ tr : $ < /etc/passwd


:star: **od**
>Translate a text file into octal and hexadecimal formats

:star: **sed**
>Explore a stream editor
+ sed 's/chocolate/strawberry/' food.txt
    + switch chocalte to strawberry ( Only for the output)
+ sed 's/chocolate/strawberry/g' food.txt
    + switch chocolate to strawberry globally
+ sed '/^$/d' food.txt
    + blank lines will be removed

:star: **grep**
>Simple text search
+ grep -i root /etc/passwd
    + **-i** for case insensitive search
+ grep -i ^root /etc/passwd
    + **^** to find word at the **start** of a line
+ grep bash$ /etc/passwd
    + **$** to find word at the **end** of a line
+ grep bash$ /etc/passwd > (newFile)
    + **>** Creates a new file or overwrites file contents with STDOUT
+ grep bash$ /etc/passwd >> (newFile)
    + **>>** Appends STDOUT to a file (will create the file, if it does not exist)
+ grep HOST /etc/*.* 2> /dev/null
    + Redirects error message to /dev/null/ (Black hole)
+ grep -d skip -i ipv[46] /etc/* 2> (fileName)
    + -d skip: skip directory , -i: case insensitive, [ ] brackets regular expression
+ grep -d skip -i rfc[1-3] /etc/services 2> /dev/null
    + [ - ]: bracket range function
+ grep -i \#\ boot[ /etc/services
    + \\: escape regular expression
+ grep -i r.ot /etc/services
    + r.ot: searches both r and ot
+ grep -i ro*t /etc/passwd
+ grep -E ro+t /etc/passwd
    + **+**, **-E** , Character present one or more times
+ grep -E ro?t /etc/passwd
    + **?**, Character present zero or one time
+ grep -E root\|shutdown /etc/passwd
    + **|** either/or pattern
+ grep -E "root|shutdown" /etc/passwd
    + **"command"**, shell quoting 
+ grep -E "(^root|^shutdown).*bash$|shutdown$" /etc/passwd
    + Grouping expression patterns with parenthesis
+ grep

:star: **|** *pipe*
+ grep nologin$ /etc/passwd | wc -l
+ sort -d: -f1,7 /etc/passwd | sort | less | 

:star: **tee**
>Directing STDOUT to two different locations
+ sort -d: -f1,7 /etc/passwd | sort | tee data.txt | less 

:star: **xargs**
>If a command doesn't accept STDIN, but you want to pipe to it, use **xargs**
+ ls test.txt | xargs -o rm -i

:star: **$(command)**
+ grep $(cat test.txt) /etc/passwd

:star: **\`command`**
+ grep \`cat test.txt` /etc/passwd

:star: **locate**
>Basic and fast command to find files
>>Uses a database(**mlocate.db)\
Database updates(updatedb)

:star: **find**
>Flexible command with many file search features
+ find /home -regex .*word.txt
+ find /etc -maxdepth 1 -name passwd

:star: **file**
>Determine a file's type

:star: **mkdir**
+ mkdir -p (DirName)/(DirName)
    + -p Creating a directory tree

## File Compression
:star: **gzip** \ **gunzip**

:star: **zcat**

:star: **bzip2** \ **bunzip2**

:star: **bzcat**

:star: **xz** \ **unxz**

:star: **xzcat**

:star: **tar**
+ -c --create: Create a tar archive by placing copies of the designated files in the designated archive
+ -u --update: Add files that were changed since an archive was created to the pre-existing tar archive
+ -v --verbose: Displays a file's name as it is added to the archive
+ -f : Designates the tar archive file to use
    + tar -cvf ( nameOftar ) ( fileName )
+ -d --compare, --diff
+ -t --list
+ -W --verify
+ -x --extract, --get
+ -O --to-stdout


:star: **cpio** copy in/out
+ ls file? | cpio -ov > archive.cpio
+ cpio -itvI archive.cpio
    + -itvl: viewing files in an archive file 
+ cpio -iv --no-absolute-filenames -I archive.cpio
    + -ivl: Extracting files from an archive file

:star: **lsblk** 
>Allows us to see the disks also called block devices currently available

:star: **dd**
+ dd if=/dev/sda of=/dev/null status=progress
>Copy while disk and sends it to the black hole

## File permission 
**-rw-r----- 1 root shadow 1275 Sept 22 11:07 /etc/shadow**
| - | rw-r----- | 1 | root | shadow | 1275 | Sept 2 11:07 | /etc/shadow |
|-------------|---------------------|------------|-------|-------|------|--------------------------|---------------|
| Object Type | File/Dir permission | Link Count | Owner | Group | Size | Modification Date & Time | File/Dir Name | 

**Object Type** 
+ (**-**) File
+ (**d**) Directory
+ (**l**) Symbolic link
+ (**b**) Block device
+ (**c**) Character device

**File/Dir Permissions**
+ **rwxrw-r--** 
    + **r** read
    + **w** write
    + **x** execute
    + **-** no permission

|rwx|rw-|r--|
|---|---|---|
|Owner Permissions|Group Permissions|World Permissions|

**Owner / Group**

:star: **groups, id-Gn**
>Viewing your group memberships

:star: **id -gn**
>Viewing your current effective group

:star: **chgrp** 
>Change group permission
+ chgrp adm file1.txt

:star: **chown**
>Change owner permission
+ sudo chown root file1.txt
+ sudo chown root:adm file1.txt
+ chown :adm file1.txt

:star: **chmod**
>Method of changing a file's permissions
+ chmod o+r file1.txt
+ chmod u+x file1.txt
+ chmod a=rw file1.txt
+ chmod u+r,g-x file1.txt
    + **u** for owner
    + **g** for group
    + **o** for others
    + **a** for owner, group, and others
+ chmod 764 file1.txt
+ chmod 700 file1.txt
    + 0 is no permission
    + 1 is execute
    + 2 is write
    + 4 is read

:star: **SUID** Set User ID
>Set on Owner level\
Runs executable file with file's owner of file's permissions
+ chmod u+s ( fileName ) + chmod u+x ( fileName )
+ chmod u+sx ( fileName )

:star: **SGID** Set Group ID
>Set on Group level\
Runs executable file with file's group of file's permissions
+ chmod g+s ( fileName )
+ chmod g+xs ( fileName )

:star: **Sticky Bit**
>Set on World level of permissions on a directory\
Allows sharing of files in a directory\
Only file's owner may delete file
+ chmod o+t ( directoryName )

+ chmod <span style="color:red">4</span>644 ( fileName )
    + SUID: 4
    + SGID: 2
    + Sticky bit: 1

:star: **umask**
>Default creation mask

+ umask 0027
    + 0 - No permissions
    + 1 - Execute permission
    + 2 - Write permission
    + 3 - Execute permission'
    + 4 - Read permission
    + 5 - Execute and Read
    + 6 - Read and Write 
    + 7 - Readm Write, and Execute

**Hard & Soft link**\
:star: **ln**
+ ln -s file1.txt file1SoftLink
    + -s: Soft link
+ ln file2.txt file2HardLink

## Processes
>A processe is a running program

:star: **ps**
+ ps --tty tty2 
    + GNU long options have two dashes
+ ps -elf 
    + Unix-style opetions have a single dash
+ ps aux
    + Berkley software distribution(BSD) options have no dashes

:star: **pgrep**
+ pgrep bash
+ pgrep -u jma
+ pgrep -au jma
+ pgrep -at tty1

:star: **free**
>Check how much ram is free
+ free -h

:star: **sleep**
>The shell will pause for assigned amount of seconds
+ sleep 3

:star: **bg**
:star: **fg**

:star: **jobs**
>A job is a process

+ **Ctrl+z / bg job#**
    + Move a job to the background
+ **command&**
    + Start a job in the background
+ **fg job#**
    + Move a job back to the foreground
+ **jobs -l**
    + How to view background jobs

:star: **1, HUP, SIGHUP**
>Terminate process, when user logs out

:star: **9, KILL, SIGKILL**
>Unconditionally kill a process

:star: **15, TERM, SIGTERM**
>Terminate a process, if possible

:star: **man -s 7 signla**
>See all signals in "Standard signals" section of the sifnal man page

:star: **ps-l PID**
>How to view a process priority

:star: **nice**
>Set process priority prior to execution

:star: **renice / top**
>Modifiy process priority


## Managing environment
:star: **printenv & echo**
+ Viewed Environment Variable settings

:star: **enc & printenv & set**
+ View all set Environment Variables
    + env | less, printenv | less, printenv HOME, set | less
+ $USER, USER, $LOGNAME
+ $EDITOR
+ $VISUAL
+ $PWD
+ $PS1
+ $HISTFILE
+ $HISTSIZE
+ $UID
+ $GROUPS, { $GROUPS [*]}
+ $BASH_VERSION
+ $HOSTNAME
+ $LANG
    + Overall locale variable
+ TZ
    + Time zone different than system's default time zone
+ LD_LIBRARY_PATH
    + list of library directories

#### Path environment variable
:star: **$PATH**
+ PATH=$PATH:(newDirectoryName)
    + For changing the PATH environment variable
#### Changing Shell prompt
:star: **$PS1**
+ PS1="My prompt:"

:star: **$PS2**
>Change the apearance of the secondary prompt
+ echo \
    + Goes into a secondary prompt
+ PS2="2nd prompt:"
+ EDITOR=/usr/bin/nvim

#### SubShell
:star: **$SHLVL**
> Shows the current level of the shell I am in

:star: **bash**
> start a subshell

:star: **export**
> Make a variable definitions survive a shubshell entry

## Storage
 **sda**
> Represents an entire disk
+ ls /dev/sda?
    + Shows how many partitions this disk have

**swap**
> Is either a partition, child partition, or a file that acts as an extension to memory

:star: **lsblk**
> Views disks, partitions, and child partitions, Explore swap space
+ lsblk -f 

:star: **free**
> Explore swap space
+ free -h

**cat /proc/partitions**
> Look at system partitions

**cat /proc/filesystems**
> Views system supported filesystem

**ls /dev/sd***
> SATA, SCSI, USB-attached drives

**ls /dev/sr***
> Optical drives

**ls /dev/hd***
> PATA disks

**ls /dev/fd?**
> Floppy disks

## Hardware
**PCI**
> Peripheral component Interconnect\
is a bus on the system, where you can add additional hardware componenets

:star: **lspci**
> View's PCIs and devices connected through them
+ lspci -vv

:star: **lsusb**
> USB connected devices

:star: **lsmod, modinfo**
> Views loaded kernel modules
+ lsmod | grep joydev
+ modinfo joydev

:star: **insmod**
> Insert a single module
+ sudo insmod /lib/modules/5.17.1-arch-1/kernel/drivers/input/joydev.ko.zst

:star: **rmmod**
> Remove a singel module
+ sudo rmmmod joydev

:star: **modprobe**
> Loads a module with its dependents

:star: **modprobe -r** 
> Unloads a module and its dependents

:star: **udev**
> Handling hot/cold plug devices
+ udevadm info
    + To view hot/cold plug devices
+ /media
    + To view automatically mounted hot plug disk location
+ ls /etc/udev/rules.d/
    + udev hot plug device rules location

**Cold Plug**
> Is one that cannot be attached to a running computer system

**Hot Plug**
> Is one that can be attached to a running computer system

## Partitions
:star: **lsblk**
+ lsblk | grep disk
+ lsblk | grep -E "sd[abc]?"

+ cat /proc/partitions
    + Displays the partitions files

:star: **gdisk**
+ sudo gdisk /dev/sdb

:star: **fdisk**
+ sudo fdisk /dev/sdc

:star: **parted**
+ sudo parted /dev/sdc

***Creating Partitions***
> Partition table\
Data structure on disk\
Managed by operating system\
Contains information such as: Partition location on disk & Partition size\
Operating system reads a disk's partition table first\

**MBR**
> Master Boot Record\
Size limit of ~2.2TB\
Partition types: Primary, Extended, Logical

**GPT**
> Globally Unique Identifier(GUID) Partition Table(GPT)\
Supports disks > 2.2TB, unlimited number of partitions\
No partition types\
Copies table to last disk sectors for protection

***Making Filesystems***

:star: **mkfs**
+ sudo mkfs -t ext4 /dev/sdb1
+ sudo mkfs.ext4 /dev/sdc2

:star: **mkswap** 
+ sudo mkswap /dev/sdc1

***Mounting Filesystems***

:star: **mount**
1. mkdir /home/jma/temp
1. sudo mount -t ext4 /dev/sdb1 temp
1. ls temp 
    + lost+found

:star: **umount**
1. sudo umount temp ***OR*** sudo umount /dev/sdb1
1. mount | grep temp

**cat /etc/fstab**

| filesystem | mount point | type | options | dump | pass |
|------------|-------------|------|---------|------|------|
+ Identify filesystm by
    + **Device file name** /dev/sdb1
    + **UUID** UUID=f2c48311-e5e5-4984-907c-83d484530a09
    + **Label** LABEL=program-42
+ **Options** are comma separated (defaults, noauto)
    + defaults: **Sets options to** async, auto, dev, exec, nouser, rw, suid
    + user: **Allows a user to mount this filesystem**
    + owner: **Allows an owner to mount this filesystem**
    + noauto: **Keeps a filesystem from automatically mounting**
+ **Dump** if not set to 0, use _dump_ utility to backup filesystem
+ **Pass** if not set to 0, use _fsck_ utility to check filesystem by priority order, such as 1 before 2

1. sudo cp /etc/fstab /etc/fstab.bck
1. sudo mkdir /program42
1. sudo vi /etc/fstab
1. sudo mount -a
1. mount | grep program42
1. ls /program42
    + lost+found
:star: **blkid**
+ sudo blkid | grep -E "sd[abc]?" (**lsblk** is way better)

:star: **systemctl**
+ systemctl -t mount list-units
> Displays systemd managed mounted filesystem

**/etc/systemd/system**
> Can view systemd customized systemd mount unit files

#### filesystem Consumption

:star: **df** 
> Disk free command 
+ df -i
> i: inodes

:star: **du**
> Individual file size
+ du -s /home
+ du -s --inodes /home

#### Tuning filesystem
:star: **mke2fs**
> Create an ext2/ext3/ext4 filesystem

:star: **tune2fs**
> Adjust tunable file system parameters on ext2/ext3/ext4 file system

#### Reparing filesystem

:star: **fsck & e2fsck**
> Check and repair ext file system
+ sudo fsck -r /dev/sdc2

