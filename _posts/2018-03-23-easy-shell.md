---
layout:  post_content
title:  "easy shell :)"
date:   2018-03-24 01:16:01 -0600
comments: true
excerpt_separator: <!---excerpt--->
---

## for your daily linux hacking

Easy Shell is a collection of useful boilerplate linux
commands for the daily life of every linux user!

All credit goes to [lucasviola](https://github.com/lucasviola/easyshell) on GitHub!

## Hey you!

This is a "go through" guide intended to help newcomers and medium Linux users on consulting useful bash commands.

This is a living web page! Which means it will be updated on a regular basis as more and more people contribute to it :)

This is not a guide, nor a tutorial for Linux, Shell or Bash. For reals. It's just a collection of some good commands, materials, tips and tricks gathered from all around the internet and presented in a nice way so you can easily find it.

Thank you and keep bashing!

## Introduction: basic linux knowledge

- This is probably the most important lesson you will ever learn on Linux: man pages are your best friend! Learn to read them. Learn to understand them. Learn to love them.

To access a man page on any linux program just type:

{% highlight sh linenos %}
 man <program>!
{% endhighlight %}

E.g:

{% highlight sh linenos %}
$ man ps
PS(1)                User Commands                     PS(1)

NAME
       ps - report a snapshot of the current processes.

SYNOPSIS
       ps [options]

DESCRIPTION
       ps displays information about a selection of the active processes.  
       If you want a repetitive update of the selection and the displayed
       information, use top(1) instead.

       This version of ps accepts several kinds of options:

       1   UNIX options, which may be grouped and must be preceded by a dash.
       2   BSD options, which may be grouped and must not be used with a dash.
       3   GNU long options, which are preceded by two dashes.

{% endhighlight %}

- To view a short information on any program:

{% highlight sh linenos %}
whatis <program>
{% endhighlight %}

- You can also find out where it is located by typing:

{% highlight sh linenos %}
whereis <program>
{% endhighlight %}

- To change user:

{% highlight sh linenos %}
sudo -u <user>
{% endhighlight %}

- To change user to superuser (root):

{% highlight sh linenos %}
sudo su
{% endhighlight %}


Attention: This is not recommended since as a superuser you have total control of your system, hence you can end up fucking it badly.

- "/" represents the root directory.

- "~" is an alias for your user's home directory, which usually is: /home/youruser/.

- "." represents the current directory

- To decompress a tarball:

{% highlight sh linenos %}
tar -vzx <compressed-file.tar.gz>
{% endhighlight %}

Note: Flag **-v** is for verbosity.

- To see your session history:

{% highlight sh linenos %}
history
{% endhighlight %}

Pretty useful stuff:

- `|` is a piping operator. It is used for inserting the output of a program into the input of another program.

E.g:

Listing all process called "init":

{% highlight sh linenos %}
ps -aux | grep init
{% endhighlight %}

- You can quickly write something into a file by doing:

{% highlight sh linenos %}
echo "any random sentence" >> any-random-file.txt
{% endhighlight %}

The '>>' operator will concatenate the sentence to the end of the file.

BE CAREFUL not to use '>' instead of '>>' since the former will OVERWRITE the content of the file instead of adding the sentence to it.

- You can call a previously used command pra typing "!" plus the initials of the said program.

For example, let us say you want to edit .bashrc and then open it to edit again:

{% highlight sh linenos %}
vim ~/.bashrc
exec bash
!vim #This will execute the last command on history with the "vim" initials
{% endhighlight %}

- `uname -a` will tell you information about your system

- `df -h` will tell you about your file system disk space

## Network

### Utils commands

Show all network interfaces

{% highlight sh linenos %}
ifconfig
{% endhighlight %}

Configure a wireless network interface

{% highlight sh linenos %}
iwconfig
{% endhighlight %}

Get more information about wireless interface

{% highlight sh linenos %}
iwlist <your_interface_here> scan
{% endhighlight %}

<!---excerpt--->
Check hardware information include about your network, this shows PCIs drivers which is installed or not

{% highlight sh linenos %}
lspci
{% endhighlight %}

Show who is connected in your network  

{% highlight sh linenos %}
nmap 192.168.0.*
{% endhighlight %}

Verify if you have any open port

{% highlight sh linenos %}
nmap <your_ip>
{% endhighlight %}

## Custom Bash

### Customize your bash cursor

The `PS1` environment variable contains the style for the bash cursor:

Export it to your ~/.bashrc file:

{% highlight sh linenos %}
export PS1='\u@\h \$'
{% endhighlight %}

This will print the following as a cursor: `user@host $`

Some formatting options can be:

{% highlight sh linenos %}
\h - The hostname, up to the first ' . '

\H - The hostname.

\n - A newline.

\t - The time, in 24-hour HH:MM:SS format.

\T - The time, in 12-hour HH:MM:SS format.

\@ - The time, in 12-hour am/pm format.

\u - The username of the current user.

\w - The current working directory, with $HOME abbreviated with a tilde.

\W - The basename of $PWD, with $HOME abbreviated with a tilde.
{% endhighlight %}

Further reading:

[PS1 Generator](http://bashrcgenerator.com/)

[Git info on bash PS1](http://mediadoneright.com/content/ultimate-git-ps1-bash-prompt)

[Bash manual](http://www.gnu.org/software/bash/manual/bashref.html)


## Tailing

### Search, save and simplify command outputs:

Bit bucket (as known as the black hole, one of the linux's special files):

{% highlight sh linenos %}
/dev/null
{% endhighlight %}

Standard input stream:

{% highlight sh linenos %}
STDIN
{% endhighlight %}

Standard outpout streams:

{% highlight sh linenos %}
STDERR and STDOUT
{% endhighlight %}

Tailing files (getting the last lines)

{% highlight sh linenos %}
tail <file>
{% endhighlight %}

Outputing whole file content

{% highlight sh linenos %}
cat <file>
{% endhighlight %}


Reading from `STDIN` to a file (stop with `CTRL + C`)

{% highlight sh linenos %}
cat > <file>
{% endhighlight %}

Reading from file to another file

{% highlight sh linenos %}
cat <file1> > <file2>
{% endhighlight %}

Reading all lines of file with line numbers

{% highlight sh linenos %}
cat -n <file>
{% endhighlight %}

Saving output to file (using nano editor)

{% highlight sh linenos %}
<command> | nano file_name
{% endhighlight %}

Searching through the output

{% highlight sh linenos %}
<command> | grep <term>
{% endhighlight %}

Displaying output in a file-like style (`less` allows searching by pressing `/`)

{% highlight sh linenos %}
<command>|less or
<command>|more
{% endhighlight %}

Preventing terminal hanging (command outputs will still be shown in the terminal)

{% highlight sh linenos %}
<command>&
{% endhighlight %}

Ignoring file output completely (note that `2 = STDERR` and `1 = STDOUT`)

{% highlight sh linenos %}
<command> > /dev/null 2 > &1
{% endhighlight %}

## File permissions

- To change the owner of a directory:

{% highlight sh linenos %}
sudo chown -R newowner:newowner
{% endhighlight %}

- To view actual files permissions

{% highlight sh linenos %}
ls -l
{% endhighlight %}

  - Example: `drwxr-xr-x`:
    - First letter is the file type:

      d          | b          | c            | p    | s      | \-
      :---------:|:----------:|:------------:|:----:|:------:|:-----------:
      directory  | block file | special file | pipe | socket | regular file

    - Second, third and fourth letters are the **user** permissions
    - Fifth, sixth and seventh letters are the **group** permissions
    - Eighth, ninth and tenth letters are the **others** permissions
    - Permissions

      r    | w     | x       | \-
      :---:|:-----:|:-------:|:------:
      read | write | execute | disable

- To change the files permissions:
  - Using letters:
    - Which users:

      u    |   g   |    o   | a
      :---:|:-----:|:------:|:--:
      user | group | others | all

    - Operators:

      \+             |        \-         |                  =
      :-------------:|:-----------------:|:----------------------------------:
      add permission | remove permission | changes permissions to the inserted

    - Permissions:

      r    | w     | x      
      :---:|:-----:|:------:
      read | write | execute

    - Example: `$ chmod a+w file` add **write** permission for **all** users
  - Using numbers
    - Permissions:

      read | write | execute
      :---:|:-----:|:------:
        4  |   2   |    1

    - Example: `$ chmod 754 file` set permission to file:

       user                  |      group     |others
      :---------------------:|:--------------:|:------:
       7                     |       5        |  4
      read + write + execute | read + execute | read


## Managing and killing processes

To list all processes on your system

{% highlight sh linenos %}
ps -aux
{% endhighlight %}

To list all processes running as root

{% highlight sh linenos %}
ps -U root -u root u
{% endhighlight %}

To list all processes owned by you

{% highlight sh linenos %}
ps x
{% endhighlight %}

Searching processes by keyword

{% highlight sh linenos %}
ps -aux | grep '<keyword>'
{% endhighlight %}

Listing it Tree style

{% highlight sh linenos %}
ps -aux --forest
{% endhighlight %}

Killing a specific process

{% highlight sh linenos %}
sudo kill -9 <PID>
{% endhighlight %}

Killing all processes except for kill and init

{% highlight sh linenos %}
sudo kill -9 -1
{% endhighlight %}

## Working with environment and variables

Listing local variables

{% highlight sh linenos %}
set
{% endhighlight %}

Listing global variables

{% highlight sh linenos %}
env
{% endhighlight %}

Printing variable content

{% highlight sh linenos %}
$ foo='This is a variable!'
$ echo $foo
{% endhighlight %}

Looking for a local variable

{% highlight sh linenos %}
set | grep foo
{% endhighlight %}

Exporting it to env

{% highlight sh linenos %}
$ export foo
$ env | grep foo
{% endhighlight %}

Useful environment variables

{% highlight sh linenos %}
- $PS1 your prompt setup
- $PATH your path setup
- $USER your current user
{% endhighlight %}

The most important files regarding your environment are:

{% highlight sh linenos %}
1. $ ~/.profile
2. $ ~/.bashrc
{% endhighlight %}

Both of them are shell scripts and contain instructions which are executed when you log in.

Permanently exporting variables to your PATH:

{% highlight sh linenos %}
echo 'export $PATH="$PATH:/path/to/file/"' >> ~/.bashrc
{% endhighlight %}

## Working with files

- Where am I?

{% highlight sh linenos %}
pwd
{% endhighlight %}

- Creating Files

{% highlight sh linenos %}
> filename
{% endhighlight %}

- Changing directories

{% highlight sh linenos %}
cd path/to/directory
{% endhighlight %}

- Moving things around

{% highlight sh linenos %}
mv -v <filename> /another/path/
{% endhighlight %}

- Deleting things FOREVER

{% highlight sh linenos %}
sudo mv -v <filename> /dev/null/
{% endhighlight %}

- Copying stuff

{% highlight sh linenos %}
cp -v <filename> <another-filename>
{% endhighlight %}

- Deleting files

{% highlight sh linenos %}
rm -v <filename>
{% endhighlight %}

- Deleting folders

{% highlight sh linenos %}
rm -vR /path/to/<folder>
{% endhighlight %}

- Updating timestamp:

{% highlight sh linenos %}
touch <filename>
{% endhighlight %}

- Listing files and directories

{% highlight sh linenos %}
ls -al
{% endhighlight %}

Notes:
- `-a` tells ls to list all files.
- Files starting with `.` are hidden files. (Remember this).

- Printing the content of a file:

{% highlight sh linenos %}
cat <filename.txt>
{% endhighlight %}

- Printing the last 2 lines of a file:

{% highlight sh linenos %}
tail -n 2 <filename.txt>
{% endhighlight %}

- Printing the first 2 lines of a file:

{% highlight sh linenos %}
head -n 2 <filename.txt>
{% endhighlight %}
