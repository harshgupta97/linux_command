# Commands

- cat - read file
- ifconfig - ip
- top - Activity monitor
- cd - change directory 
- pwd - print working directory
- ls - list
- su - switch user
- head - first page of the list result
- tail - last page of list result

## list command

- ls -ltr - timely order
- ls -l - list all with details

## Change password 

- passwd userid

## Creating files and directories

- touch - will create an empty file
- cp
- vi

## Create directory

- mkdir

## Copying directories

- cp -R

## Find files and directory

- find
    ```
    find . -name "search key"
    ```
- locate
    ```
    locate searchkey
    ```
    short and faster search as it create a db

## soft and hard link

to get inode number
```
ls -ltri
```

```
# hard
ln <filename> <linkname>

# soft
ln <filename> <linkname>
```

## Manual

```
man <command>
```

## Permissions

```
chmod <group(a|u|g|o)><add(+)/remove(-)><permission(rwx)>
```

## File ownership

```
chown <root|<username>> <filename|directory>

chgrp <root|<username>> <filename|directory>
```

NOTE: if a user is having write permission for a directory anything inside that directory that user dosen't own can do a write operation, if the user dosen't have write permission for that directory then he can not delete the file

## ACLs


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

## Adding text to files

echo > overwite the file
echo >> write to next line in the same file

## Input and Output redirects

- stdin - <
- stdout - >
- stderr - 2>

## Standard output to a file

```
# like >
echo "Hello World" | tee hello

# output to multiple file
echo "Hello World" | tee file1 file2 file3 ... filen

# like >> it will append
echo "New Hello" | tee -a hello

tee --help
```

## Pipes `(|)`

```
<command1> <argument> | <command2> <argument>
```

## File maintainance command

- cp - copy file
- rm - remove the file
- mv - it will move and rename the file
- mkdir - 
- rmdir or rm -r
- chgrp
- chown
```
chown <>:<> file
```

## File display commands

- cat - View entire content of file

- more - Views content of a file one page at a time
NOTE: it will autoclose

- less - View large text file, log file and configuration files (j or down arrow - next, k or up arrow - previous)
NOTE: it will not autoclose

- head - few top 10 line in a file
```
head filename

head -<number of lines> filename
```
- tail - it will give last 10 line in a file

```
tail filename

tail -<number of lines> filename
```

## Filters / Text processors commands

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

