---
layout: post
title:      "Linux Terminal Commands "
date:       2021-05-26 18:01:44 -0400
permalink:  top_linux_terminal_commands_to_remember
---


As I am getting ready to finish the software engineering course at Flatiron school, I  can recall many memories of when I just started out in this journey. So many things to learn, and so many things to remember!

In this blog, I wanted to share some of the most frequently used linux terminal commands that can be useful to both beginners and advanced users. I have listed some of the commands that I found myself using the most.

One of the best tools for a developer is the command line. Once you get comfortable with it, you will be able to use it to help make the system more efficient and manageable. 

**`ls`**

This is the most commonly used command. It lists out all the files present in the current working directory. You can also list the files from a specific folder using `$ ls ./myFolder` 
If you pass in a `-al` flag like so`ls -al`, it will list out all the  files including the hidden ones, along with their file permission.

**`pwd`**

pwd stands for Print Work Directory and it shows the the directory you are currently in. This is one of the handiest Linux terminal commands.

**`cd`**

Change Directory. This command provides a standard method to browse the entire filesystem of your device. It is one of the few commands that you are bound to use when using a Unix system.


**`echo` - `echo "hello world"`**

This command prints out the text to the command-line interface.


**`touch` - `touch mynewfile`**

This command allows youto create any file. Use this commnad with the filename you want to give to the file.


**`mkdir`  - `mkdir newFolder`**

This command is used to create directories. You can also create multiple directories with this command as by passing in more than one directory `mkdir  dir1 dir2 dir3` .

**`rmdir`**

The opposite of `mkdir` command, this command allows you to delete specific folders from your system without any hassles. 

**`cp`**

The `cp` command tells your machine to copy a file or directory from one folder to another. You can copy multiple files to a directory right from your terminal with this awesome command.

**`mv`**

Just like `cp`, you can use the `mv` command to move either single or multiple files from one location to another. 

**`grep`**

`grep` is also known as the search command. It is among the most powerful regular expression terminal commands you can use when searching for patterns inside large volumes of text files. It will take the pattern you are looking for as input and search the specified files for that particular pattern.

**`man` - `man  commandName`**

This command displays you a manual about specific command. This is very helpful when learning new commands.

**`uname`**

This command is an elementary Linux command for obtaining system informaiton like name, version, and other system-specific details. You can quickly check your OS and kernel version with this command.

**`ps`**

This command will display all the processes that are currently being run by your machine. This command is considered as one of the basic and best Linux monitoring tools available for Linux nerds.

**`kill`**

The kill command is a powerful way to stop processes that are stuck due to resource constraints. 

**`cat`**

This command is used to create new files, view file contents in the terminal, and redirect output to another command-line tool or file.

**`which`**

The which command is pretty useful if all you are trying to search are executable files. This handy little terminal command takes specific parameters and seraches for binary files in the $PATH system environment variable based on them very effectively.

**`locate`**

The locate command is used for finding the location of a specific file. It is very straight forward.

**`clear`**

This command is handy to clear out your existing terminal screen.

**`sort`**

Whenever you find the need to sort out a file in an alphabetical or reverse manner, utilize this command.

**`sudo`**

This is a very important command in the Linux world. It lets non-priviledged users access and modify files that require low-level permissions. It is often used to access root from your regular account.

**`chmod`**

The `chmod` command like the `sudo` command is a very powerful command. It is used to change or modify the access permissions of system files or objects.
Root access is required to run this command.

**`chown`**

This command is very similar to the `chmod` command and requires root access as well, but instead of changing access permissions, it allows users to change the ownership of a file or directory.

**`man`**

This command is very useful to get you familiar with Linux commands. When used with another command name, it lists the documentation page of that command.




