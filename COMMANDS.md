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

- `awk`

```
// check version
awk --version

// list 1 field from a file
awk '{print $1}' file

// list 1 and  3 field of ls -l output
ls -l | awk '{print $1, $3}'

// last field of the output
ls -l | awk '{print $NF}'

// search for a specific word
awk '/Jerry/ {print}' file

// output only 1 field of /etc/passwd
awk -F: '{print $1}' /etc/passwd

// replace words field words
echo "Hello Tom" | awk '{$2="Adam"; print $0}'

// replace words field words
cat <filename> | awk '{$2="Imran"; print $0}'

// get lines that have more then 15 byte size
awk 'length($0) > 15' <filename>

// get field matching <key> in <path>(/home/)
ls -l | awk '{if($9 == "<key>") print $0;}'

// number of fields
ls -l | awk '{print NF}'
```

- `grep/egep`

```
// version
grep --version

// help
grep --help

// search for a keyword from a file
grep <keyword> <file>

// search for keyword and count
grep -c <keyword> <file>

// search for a keyword ignore case-sensitive
grep -i <keyword> <file>

// Display the matched lines and their line numbers
grep -n <keyword> <filename>

// Display everything but the keyword 
grep -v <keyword> <file>

// search for a keyword and then only give the first field
grep <keyword> <file> | awk '{print $1}'

ls -l | grep Desktop

// multiple keywords
egrep <keyword1|keyword2> file

```
NOTE: We can mix multiple flags together
```
grep -vi
v = opposite
i = case insensitive
```

- `sort/uniq`

```
// version and help
sort --version or sort --help or man sort

// sort file
sort <filename>

// sort in reverse order
sort -r <filename>

// sort by field number
sort -k<column number> <filename>

// remove duplicate
uniq <filename> it will not work if the list is not sorted

// always sort first before using uniq their line numbers
sort <filename> | uniq

// sort first then uniq and list count
sort <filename> | uniq -c

// display only duplicate
sort <filename> | uniq -d
```

- `wc`

```
// check version OR help
wc --version OR wc --help OR man wc

// check the line count, word count and byte count
wc <filename>
// output -> {lines} {words} {size} {filename}

// Get the number of line
wc -l <filename>

// Get the number of word
wc -w <filename>

// Get the number of byte
wc -c <filename>

// wc on directory is not allowed

// number of files
ls -l | wc -l

// number of keyword lines
grep <keyword> | wc -l
```

## Compare Files

```
diff <filename1> <filename2>

cmp <filename1> <filename2>
```
## Compress and Uncompress files

```
tar cvf <tarfilename>.tar <source>

tar xvf <tarfilename>

gzip <filename>

gzip -d OR gunzip <filename>
```

## Truncate file size

```
truncate -s <size> filename
```

## Combining and Splitting files

```
cat <filename1> <filename2> <filename3> > <outputfile>

split file4

eg: split -l 300 file.txt childfile

split file.txt into 300 lines per file and output to childfilea, childfileb and childfilec
```

## Executing multiple commands with `;`

```
ls ; pwd ; whoami
```

