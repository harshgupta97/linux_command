# What is file system?

- it is a system used by an OS to manage files. It controls how data is saved or retrived.

- types of file system:
    - ext3, ext4, xfs, NTFS, FAT

- description:
    * /boot - contains files that is used by boot loader(grub.cfg)
    * /root - root user home directory. it is not same as /
    * /dev - system devices(e.g. cdrom,flashdrive, keyboard,mouse). Linux considered these devices as files.
    * /etc - configuration files
    * /bin -> /usr/bin - everyday user command
    * /sbin -> /usr/sbin - System/filesystem command
    * /opt - optional add-on application (not part of os apps)
    * /proc - running process (only exis in memory)
    * /lib -> /usr/lib - C programming library needed by files and apps
        ```
        strace -e open pwd
        ```
    * /tmp - directory for system files 
    * /home - directory for user 
    * /var - system logs
    * /run - system daemons that start very early (e.g. systemd and udev) to store temporary runtime files like PID files
    * /mnt - to mount external filesystem (e.g. NFS)
    * /media - for cdrom mounts

## File and directory properties

```
ls -l
```

- if start with l, it means it is a link
- if start with d, it means it is a directory
- if start with neither, then it is a regular file

## Linux files types

- `-` - regular files
- `d` - directory
- `l` - link - special file that points to other files or directories
    there are two types of link
    - hard
    - soft
- `c` - special charecter device files(peripheral)
- `s` - socket - files used for network communication between processes
- `p` - named pipe file, FIFO files are used for IPC (inter process communication)
- `b` - block devices

## what is root?

There are three types of root in linux system
- Root account - root is an account or username on linux machine and it is the most powerful account which has access to all commands and files.
- Root as / - the very first directory in linux is also referred as root directory
- Root home directory - the root user account also has a directory located in 
/root which is called root home directory.

## Filesystem paths
- absolute path
    start with /
- relative path
    do not start with /


## Difference between find and locate command

locate use a pre built database, which should be regulary updated, while find iterate 
over a filesystem to locate file

to update localdb use command `updatedb`

## Wildcards

A wildcard is a character that can used as a subsitute for any class of characters in a search

- `*` represent zero or more character
```
rm -rf abc*
```
any thing that match the above


- `?` represent a single character
```
ls -l ?bc*
```

- `[]` represent a range of character
```
ls -l *[cd]* | more
```

- `{}`
above will create 9 file with name abc1-xyz and so on
```
touch abc{1..9}-xyz
```

## Soft and Hard links

- inode -> pointer or numbder of a file on a hard disk
- soft link -> Link will be removed if file removed or renamed
    if the source file is deleted the link will not be removed automatically,
    need to remove it manually 
- hard link -> deleting, renaming or moving a source file will not affect the hard link
    NOTE: Hard link only work within the same partition
    
link is like a shortcut just like in windows

```
ln
ln -s
```

NOTE: You can not create a soft and hard link with the same in the same directory


## Linux command syntax

- command options and argument

commands typically have syntax

    commands option(s) argument(s)

Options:
- Modify the way that commands works
- Usually consists of a hyphen or dash follwed by a single letter
- some commands accept multiple options which can usually be grouped together after a single hyphen

argument:
- most commands are used together with one or more argument
- some commands assume default argument if none supplied
- argument are optional for some commands are required by others

## File permissions(using letters)

UNIX is a multi-user system. Every file and directory in your account can be protected from or made
accessible to other user by chaning its access permissions. Every user has responsibility for controlling
access to their files.

Permission to file or a directory may be restricted to by types

- There are three types of permission
    - r - red
    - w - write
    - x - execute

- Each permission (rwx) can be controlled at three levels
    - u user = yourself
    - g group = group of people in a project
    - o others = everyone on the system

- File or directory can be displayed by running `ls -l` command

    -rwxrwxrwx

- Command to change permission

chmod

- Directory have x(execute) as permission, because we can cd into a directory

## File permissions using(number)

0       No permission
1       execute
2       write
3       execute+write
4       Read
5       Read+execute
6       read+write
7       read+write+execute

## File ownership

- There are two owner of files and directory
    User and group

- Command to change file ownership
    chown and chgrp
    - chown change the ownership of a file
    - chgrp change the group ownership of a file

- Recursive ownership change option(cascade)
    -R

## Access control list

- What is ACL?
Access control list (ACL) provides an additional, more flexible permission mechanism for file system. It is design to assist with the UNIX file permission. ACL allows you to give permissions for any user or group to any disc resource.

- Use of ACL:
    * Think of a scenario in which a perticular user is not a member of group created by you but still you want to give some read or write access, how can you do it without making user a member of group, here comes in picture Access Control List, ACL helps us to do this trick

    * Basically, ACLs are used to make a flexible permission mechanism in linux.
    * from linux man pages, ACLs are used to define more file-grained discretionary access rights for files and directory.
    * Commands to assign and remove ACL permission are:
        - setfacl
        - getfacl

- List of commands for setting up ACL:

1. To add permission for user
```
setfacl -m u:<username>:rwx <file path>
```

2. To add permission for a group
```
setfaclt -m g:<group>:rw <file path>
```

3. To allow files or directory to inherit ACL entries from the directory it is within
```
setfaclt -Rm "entry" <file path>
```

4. To remove a specific entry
```
setfacl -x u:user <file path>
```

5. To remove all entries
```
setfaclt -b <file path>
```

NOTE:
* As you assign the ACL permission to a file/directory it adds + sign at the end of the permission
* setting w permission with ACL does not allow to remove a file


```
user:<all|specific>:rwx
```

## Help commands

```
Whatis <command>
<command> --help
man <command>
```
## Tab completion and arrow key


## Adding text to files (Redirects)

- 3 simple ways to add text to files
    * vi
    * Redirect command output > or >>
    * exho > or >>

## Input and output redirects

- There are 3 redirects in linux
    1. Standard input `(stdin)` and it has files descriptor number as 0
    2. Standard output `(stdout)` and it has file descriptor number as 1
    3. standard error `(stderr)` and it has file descriptor number as 2

- Output `(stdout)` - 1
    * By default when running a command its output goes to the terminal
    * The output of a command can be routed to file using > symbol
        E.g:
        ```
        ls -l > listings
        pwd > findpath
        ```
    * If using the same file for additional output or to appen to the same file then use >>
        E.g:
        ```
        ls -la >> listing
        echo "Hello World" >> fidpath
        ```

- Input `(stdin)` - 0
    * Input is used when feeding file content to a file
        E.g:
        ```
        cat < listings
        mail -s "Office memo" alluser@abc.com <memoletter
        ```

- Error `(stderr)` - 2
    * When a command is executed we use a keyboard and that is also considered (stdin - 0)
    * That command output goes on the monitor and that output is (stdout - 1)
    * If the command produced any error on the screen then it is considered (stderr - 2)
        E.g:
        ```
        ls -l /root 2> errorfile
        telnet localhost 2> errorfile.
        ```

## Standard output to a file `tee`

- `tee` command is used to store and view (both at the same time) the output of any command

- The command is named after the T-splitter used in plumbing. It basically breaks the output of a program so that it can be both displayed and saved in a file. It does both the task simultaneously, copies the result into the speicified files or variables anf also display the result.

## Pipes

A pipe is used by the shell to connect the output of one command directly to the input of another command

The symbol for pipe is the vertical (|). The command syntax is

```
<command1> <argument> | <command2> <argument>
```

## Filters / Text processors commands

- `cut`

```
# Does not work
cut filename

// check version
cut --version

// List one character
cut -c1 filename

// pick and choose character
cut -c1, 2, 4

// list range of character
cut -c1-3 filename

// List specific range of character
cut -c1-3, 6-8 filename

// List by byte size
cut -b1-3 filename

// List first 6th column seperated by:
cut -d: -f 6 /etc/passwd

// List first 6th and 7th column seperated by:
cut -d: -f 6-7 /etc/passwd

// Onyl print user permission of files/dir
ls -l | cut -c2-4
```

- `grep|egrep`

What is grep?

The grep command which stands for "Global regular expression print" process text line by line and prints any lines which match a specified pattern.


