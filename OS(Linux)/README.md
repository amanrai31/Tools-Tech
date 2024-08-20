# Linux (Numeric points are commands)

Kernel allows software to communicate with hardware, LINUX is just name of kernel inspired by MINIX & UNIX. Open source (1991).
GNU Coreutils(core tools) + kernel = Linux/GNU.

Distributions of linux-
1. Debian- (Ubuntu, Kali linux, elementry OS)
2. RedHat- CentOS, Fedora
3. Arch
4. Slackware

We can use VirtualBox for Ubuntu Desktop

The z shell of Mac OS is similar to bash but not the same. We have many shell but Bash is main one for linux. Bash is avilable on Linux, on windows through WSL & also on MacOS.

## Terminal terms

-  CLI - Where we enter text commands
-  Shell - software that interprets command & run.
-  Terminal - Shell runs inside terminal.

## General syntax of command - ` command options argument `
=> `ls -l -a -h` OR `ls -lah`
Here ls = list, -l = more details about file, -a = hidden file too, -h = size in bytes.

Note : Spacing and spelling matters also command should come first before options and arguments.

## Some shortcuts for terminal-
1. man ls          - (description- man page documentation)
2. apropos list    - (search)
3. tab btn         - (autocomplete)
4. ctrl + a        - (beginning of line)
5. ctrl + e        - (end of line)
6. ctrl + left     - (move left 1 word) || ctrl + right     - (move ri8 1 word)
7. ctrl + shift + c (COPY) ||  ctrl + shift + v(PASTE) || ctrl + c(CLOSE) || ctrl + l (CLEAR) || upside arrow
8. ctrl + r        - (Search command and history)

## File system
1. root `:/` - highest level of file system, containes all other directories.
2. home ` ~ ` - user personal file.  (~/Desktop == /home/Desktop)

/etc   (common config).
/bin, /sbin (common programs).
/lib  (shared lib & modules).
/dev, /proc, /sys (kernel & system info).

- Absolute path (/home/aman/Desktop)
- Relative path (..Desktop) [ e.g. current dir=Picture(parent is home) & want to go in Desktop(parent is home) ]

1. `cd "Exercise file` OR `cd Exercise\file`
2. `ls -r Desktop` (Go recursively - looks at all subfolders)
3. `cd` (takes to /home)
4. `mkdir Desktop/folder1 Desktop/folder2` -(making multiple folders)
5. `rm emptyFolder` (deletes empty folder only)
6. `rm -r someFolder` (deltes any folder - works recursively )
7. `cp /Desktop/data.txt /Desktop/folder1/` ( cp fileToBeCopied targetDirectory)
8. `mv /Desktop/data.txt /Desktop/folder2/`  (mv command works 2 ways- 1. To move file. 2. To rename file -Here we are moving )
9. `mv /Desktop/data.txt /Destop/newData.txt` (Here we are renaming data.txt)

Note : `wildCards - (* and ?)` (* for all and ? for selected one) e.g. `mv Desktop/marketing/* Desktop/hr`- move all files inside maketing to hr folder.

10. ` find . -name "poe*" ` (files having poe and last letters could be anything) (dot means - in current dir)
11. ` find /home/Desktop -name "*am*" ` (file name containing "am" )

12. `ls -l filename` OR `stat filename` - check current permission/all about that file.
13. ` cat data.tx` (content of data.txt - not for directories) 

## MultiUser envionment (Modern linux supports multiuser facility)

Normal user - Can modify their own file, but can not make system wide changes.
SuperUser/RootUser - Can do both. (SuperUser home directory is root)

Note : Not reccomended to use the root acc. for normal user. Admistrator can borrow root's privilages using sudo command.

su command - set user/ switch user

1. `ls /root` (normal user cannot do it.)
2. `sudo ls /root` ("snap"-  this is content of root.)
3. `sudo -s` (use root shell as superuser)
4. `sudo -k` (give upadmistrator privilages)

## File Permissions (Octal file permission, symbolic file permission)

#### 1. Octal file permission
(rwx- Read,write, execute)

rwxrwxrwx - 1st 3 letters are for user, 2nd 3 are for group, 3rd 3 are for others

|          | Read     | write    | execute | result |
|----------|----------|----------|---------|--------|
| user     |   r       | r       |   x     |  7     |
| group    |   r       |   -     |   x     |  5     |
| others   |   r       | -       | -       |  4     |

- 754 (rwxr-xr--)  --(user-read,write,execute | group- read,execute | other-read)
- 644 (rw-r--r--)
- 755 (rwxr-xr-x)

#### 2. Symbolic file permission (add,assign,subtract)

- `u+rwx` - giving all permission to User (for group- `g+rwx` | for others- `o+rwx`)
- `o=r` - giving only read permission to others
- `o-rwx` - no permission to other
- `a=rwx` - all permission to all.

#### Commands related to permissions

1. `chmod 666 test.sh` = `chmod a-x test.sh` = `chmod -x test.sh` (Snitch execute permission from all)  . NOW--
2. `chmod 266 test.sh` = ` chmod u-r test.sh` (snitch read permission from user)






















Note : `nano test.sh` edit this file in nano text editor.