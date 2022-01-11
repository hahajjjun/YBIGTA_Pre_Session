# [2021 Summer] Linux CLI Crash Course

Created: 2021년 7월 30일 오후 2:14

# Objective

- Introduction to LINUX CLI as a backend developer
- Working with and writing simple bash scripts
- Understanding common Linux commands and their use
- Learning about common shell config files

# Linux

- Kernel : Hardware
- OS tools : Tools to interact with hardware
- Distributions : Third party applications

# Linux Kernel

- Core of any linux distribution
- Bridge for HW-SW
- Manages HW

# Tools(E.G. gcc compiler)

- Uses the kernel to interact with hardware
- GNU/Linux is an Operating System : GNU is a collection of these tools

# Distributions

- Packages the OS with package managers
- Different goals in mind
    - Kali Linux, CentOS, Ubuntu, Alpine

# Practical Linux CLI

- ubuntu Linux distribution based
- **root**@<username>:/#
- **root** means access to everything
- if you sign with another user : #(hash) → $(dollar sign)
- echo "<your text>" returns <your text>, without any quotes : this is useful when you want to print <your text> with special meaning(e.g. command sentences)
- Shell = A program that runs your command : bash, zsh, fish shell....

# Navigating Directories

- Absolute path and Relative path
- ^C(ctrl+C) means quickly exiting current command : not execute the command
- pwd means echoing current directory
- IF I'm inside the <root> folder,
    - cd /root
        - go to /root directory = same folder
    - cd root
        - No such file or directory because there is no root folder inside a current folder(=root)

# ls : listing

- ls means listing the folders and files inside the current directory
- Depending on the shell, shell can 'highlight' or 'bold' according to the directory
- ls -l (equivalent to ll) allows to list all the files with a lot more details about particular file
- drwxr-xr-x   vs   rw-rw-r—  vs   lrwxrwxrwx
    - starts with 'd', 'r', 'l'
    - 'd' means directory
    - 'l' sometimes can be directory(a little bit tricky) : 'l' just points to some other file or some other folder inside the directory

# cat  : reading file

- most common way to read some file
- available in bash, zsh, fish....
- cat <file name> to read file

# less : browse bigtext

- bigtext sometimes overwhelm the whole window
- less <file name> → pagination of big text
- use arrow keys to scroll
- q() means exiting the file

# mkdir : make directory

- mkdir <folder name> → creates directory(folder) named <folder name>
- how to make nested directories at once
    - mkdir -p <folder name 1>/<folder name 2>/<folder name 3>
    - -p is a **flag :** flag is an extra information to a command when you are executing it

# rm : remove file and folders

- rm <file name> → removes file
- rm -r <folder name> → go into the folder and deletes all files recursively

# cp : copying file and folders

- copy file into another location or copy file into same location with another name
- cp <old file name> <new file name> → copy file into same location with another name
- copying folder needs '-r' flag to recursively copy all elements inside the folder
    
    ```bash
    mkdir folder1
    cp -r folder1/ folder2
    ```
    
- copying file to another directory
    
    ```bash
    cd folder1
    touch file1
    # ls returns file1
    cp file1 folder2
    # then file1 is also in folder 2
    ```
    

# mv : move file and folders

- also used for renaming stuffs
- mv <file name 1> <file name 2> → <file name 1> changed to <file name 2>
- mv <file name> <folder name or directory> → move <file name> to <folder name>
- mv <folder name 1> <folder name 2> → move <folder name 1> inside the <folder name 2>

# which : determine where a particular binary is located at

- commands like 'pwd', 'echo 123', 'ls' also exists as a binary code which is executable by CPU
- so this code(binary file) for that is located in /bin folder.
    
    ```bash
    ls #ls is equivalent to...
    /bin/ls #inside /bin folder, there are all sorts of binaries.
    ```
    
- executing a specific command means executing a binary file inside the /bin/<command name> directory
- which returns the directory where specific command is located in.
    
    ```bash
    which cd
    # echos /usr/bin/cd
    ```
    

# find : searching command

- just like SQL query
    
     
    
    ```bash
    $find / #all
    $find / -type f #file
    $find / -type d #dir
    $find / -type f -size +5M #size
    $find / -type f -perm 644
    $find / -type f -mtime +5d #date
    $find / -type f -exec ls -l {} \; #exec : link two commands in a row
    # upper code means find all files inside current directory and print in 'ls -l' form
    ```
    

# grep : match very complex patterns with the use of REGEX

- find the word 'zip' inside the foldername or filename
    
    ```bash
    $grep foo test.txt #find foo inside test.txt
    $grep foo * #find foo at all the files inside current dir
    $grep foo * -r #find foo recursively
    $grep foo test.txt -A 3 #foo 가 있는 line 뒤 3line 함께 출력
    $grep foo test.txt -n #foo 가 있는 line의 line number 함께 출력
    $grep foo test.txt -rn #recursively line number 함께 출력
    ```
    
- methods using stdin
    
    ```bash
    $ps aux | grep foo test.txt # foo가 있는 line 출력
    $ps aux | grep foo | grep -v 'bar' # foo가 있는 라인에서 bar는 빼고 출력
    
    ```
    

# wc :

# nano : edit files within the terminal

- allows quick edit
- nano, vim are quick editors
- **nano** match.py allows you to edit match.py file
- ctrl + X to Exit
- ctrl + O to WriteOut (Save)
- creating new file by using new name, which does not exit

### Copy & paste in nano

- press ctrl + 6 at the cursor where you want to start cutting : change mode to "Mark Set", allows your cursor to browse around the text
- the last character which is colored will not be copied
- Hello World : "Hell" is only copied
- ctrl + K : cut text
- ctrl + U : uncut text(paste text)

### Search nano

- ctrl + W : switch to search thing
- search : <word you wanna search> will lead to the first matching word inside the file.
- to search next matching word, press ctrl + W again and enter(nano will remember the last serach query)
- nano search does not distinguish lowercase and uppercase.
- move to the end of the line : ctrl + E
- move to the starting of the line : ctrl + A
    - this is nano / terminal shortcut!!

# Shell Scripting Introduction

- You also can program inside the bash shell, just like python or c
- It's also possible to execute bash scripts

### Running Simple Bash Script

- You can execute script written in nano editor via bash command.
    
    ```bash
    nano script
    	# nano editor : script
    	# echo "this is my first script"
    bash script
    	# bash command executes 'script' file
    	# finally executes the text written inside the script file
    	# which prints "this is my first script" to the shell terminal window
    ```
    

### Variables In Bash

- declare a variable, and then use it by appending a $(dollar sign) in front of the variable name
- Caution!!! When you declare variable, there should be no blanks (" ")
    
    ```bash
    # nano filename : 'new'
    myvariable="this is a	cool string" 
    # wrong example :
    # myvariable = "this is a cool string"
    echo $myvariable
    # bash new => then prints "this is a cool string"
    # of course, without quotes
    ```
    

### Arguments In Bash

- pass arguments when executing a script via $ sign
    
    ```bash
    # script name : newargument
    echo $1 $2 $3 $4
    # four arguments
    bash newargument "hi" "dude"
    # returns "hi dude"
    bash newargument "hi" "dude" "is" "this" "working?"
    # it only returns four argument
    # returns "hi dude is this"
    ```
    

### Reading Stdin

- read command enables standard input
    
    ```bash
    # script name : newread
    echo "Enter your name : "
    read name
    # double quotes enable you to parse vairable
    echo "Your name was: $name"
    # while single quotes mean string
    echo 'Your name was: $name'
    # this returns "Your name was : $name"
    # of course, quotes are neglected
    ```
    

### Building Username Password

- read -p command enables input without echoing
- read -sp command enables silent input
    
    ```bash
    read -p "Username: " username
    read -sp "Password: " password
    
    echo "Your username is $username"
    echo "Your password is $password"
    ```
    

### If Else in Bash

- if ~ else ~ fi statement
    
    ```bash
    read -p "Username: " username
    read -sp "Password: " password
    
    if [ "$username" = "admin" ] && [ "$password" = "admin" ]; then
    echo "Hello, $username"
    else 
    echo "Your login is invalid"
    fi
    ```
    

### Logical Operators And Status Codes

- echo $? command returns the status code
- generally status code 0 means that last command was executed properly, while nonzero status code(e.g. 127) means that bash failed to execute the last command
    
    ```bash
    read -p "Username: " username
    read -sp "Password: " password
    
    if [ "$username" = "admin" ] && [ "$password" = "admin" ]; then
    echo "Hello, $username"
    exit 0
    else 
    echo "Your login is invalid"
    exit 1
    fi
    
    # if username = admin and password = admin
    # scrirpt will echo "Hello, admin"
    # And then echo $? command will return 0
    # else echo $? command will return 1
    ```
    
- application : you can link two statements with double ampersands(&&) or (|| : or symbol)
    
    ```bash
    bash script && echo "everything went right"
    # script is the code above this block
    # this command will echo "everything went right"
    # if and only if script returns exit code zero
    bash script && echo "everything went wrong"
    # this command will echo "everything went wrong"
    # if and only if script returns exit code 1
    ```