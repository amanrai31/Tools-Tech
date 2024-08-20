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

/etc   (common config) |
/bin, /sbin (common programs) | 
/lib  (shared lib & modules) | 
/dev, /proc, /sys (kernel & system info)

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

## The UNIX philosophy (Standard GNU coreutils follows this pattern)
- Tools should do only 1 thing. 
- Tools designed to be used together in diff ways - PIPES
- Tools should use text interface (Input, output in text format)


#### PIPES
Take output of one command & send it to another. Integrated individual specialzied tools together. (NOTE: Order matters with PIPES)

E.g. of pile command - `cat users.txt | sort -u`


## Text files

Search text in file (grep- case sensitive)

1. `grep "the" poem.txt` - find "the" in poem.txt
2. `grep -n "the" poem.txt` - find "the" in poem.txt with line number.
3. `grep -in "the" poem.txt` - case insensitive "the" with line number.
4. `grep -iv "the" poem.txt` - drop line with "the" 
5. Learn regular expression with grep. `grep -E "[1 2 3]" report.txt` -(show lines containing 1,2 or 3)
6. View file with `cat`(content), `head`(start few lines), `tail`(last lines) & `less`(readable).
7. Manipulate text with `awk`(various operation on text file) , `sed`(replace, insertion, deletion) & `sort`(sorting text file)

#### Editing text with vim/vi (Vim starts in command mode when you open a file)

- Insert mode of vim (editor mode only)
- command mode (all commands can be given here only)

1. `vim sometextfile.txt` - open existing file in vim
2. `shift + i` -to go insert mode
3. `:w sometextfile.text` save the file
4. `:wq` save and exit
5. `:q!` save without exit
6. Press `esc` btn to go back in command mode

Note: We can use nano to edit text files [less features than vim].

## tar (cvf, caf, xf) and zip(zip, unzip) archives

tar(orignal, gz, bz2)

1. `tar -cvf console.tar "jecs console"` creates orignal tar file=> console.tar-(file to be created), jecs console(target file).
2. `tar -caf console.tar.gz jecs\console` - creates gz compression
3. `tar -caf console.tar.bz2 jecs\console` - creates bz2 compression
4. `tar -xf console.tar.bz2 ` - extract in current working directory
5. `tar -xf console.tar.bz2  /Desktop/newProject/` - expract in target folder /Desktop/newProject/

zip files (cross plateform friendly) **
1. `zip console.zip jecs\console` - make a zip file of jecs console with name console.zip
2. `unzip console.zip ` - unzip in working directory
3. `unzip console.zip /Desktop/JECS` -unzip in target folder Desktop/JECS.

## Environment variables and path

PATH environment variable is location which shell will search for executable programs, when installing software  it goes to PATH variable(pakage manager does this) if not then we have to add it to PATH variable. `nano ~/.bash-profile` (Shell scripting).

## Install/update software with package manager
- `APT`- Debian distribution uses APT(Advance package tool) as package manager. (.deb)
- `YUM` OR `DNF` - Redhat distribution
1. `apt search softwareName` to search
2. `apt show softwareName` more details
3. ` sudo apt update`  update software repositories

## Random system level stuff

-  `uname -r` kernel version
-  `cat/etc/*release` info about ubuntu
-  `df -h` free disk space 
-  `free -h` RAM space
-  `cat/proc/cpuinfo` -processor, cpu info
-  `lshw` -info about hardware component
-  `ip a` IP address
 
-  `>` use for redirection(Beware- overrides the contents of current file )
-  `\` to change line in CLI, if space in folder name

1. `cat auth.log | grep "input_userAuth_update" | awk '{print $9} | sort -u  >  users.txt` => 1-look at content of auth.log, 2- search for "input_userAuth_update", 3- print the 9th word of line, 4- sort alphabetically, 5- redirect the result, 6- redirect to a file name "users.txt"
2. `ssh -i .ssh.id_rsa ubuntu@10.12.111.234` => path of private key, VM username, VM IP









Note : `nano test.sh` edit this file in nano text editor.