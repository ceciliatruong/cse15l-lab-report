# Week 1 Lab Report
## Installing VSCode
1. To install VSCode, visit this [download link](https://code.visualstudio.com/download). It should send you to this page below, and you should download whichever version that is compatible with your device. I'm currently working on a Windows system, so this tutorial will be catered toward that!
![Image](/images/vscode%20download%20page.png)

2. After installing the file to your computer, launch the file and it should proceed to setup VSCode on your device. I already have VSCode installed onto my laptop prior to this, so I cannot assist with this part. As for a reference, this is what my program looks like when I launch it.
![Image](/images/my%20vscode%20home%20page.png)
## Remotely Connecting
1. In order to make sure you can access your course-specific account, you need to install the OpenSSH client onto your device if you have a Windows.
    * First, open up your Settings on Windows and navigate to the Apps section.
    * Then, go to the Optional features section and search up "OpenSSH Client" into the search bar to check if you have it installed. 
    * If it doesn't show up, click on the "View Features" button next to "Add an optional feature", search up "OpenSSH Client", and install. This is done correctly if "OpenSSH Client" shows up under the installed features portion.
    ![Image](/images/openssh.png)
2. Open up VSCode and launch the terminal by either going under the Terminal tab -> New Terminal or using the command (Ctrl + Shft + `). In the terminal, type in the following command with your course-specific account. I am using my course-specific account as an example below.
    * note that the only varying element of the format is cs15lfa22__@ieng6.ucsd.edu

```
ssh cs15lfa22bh@ieng6.ucsd.edu
```

3. The terminal will prompt you to enter the password which should be the one that you chose when you reset your password. A successful login will look like this:

    ![Image](/images/ssh%20login.jpg)

## Running Some Commands
Here are some of the commands that I've ran in the terminal as well as some brief descriptions of what they do.

```
[cs15lfa22bh@ieng6-202]:~:28$ cd ~
[cs15lfa22bh@ieng6-202]:~:29$ cd
```
`cd` changes the directory you're currently in to whatever directory you set as the argument after the command.
```
[cs15lfa22bh@ieng6-203]:~:19$ ls
hello.txt  perl5

[cs15lfa22bh@ieng6-203]:~:20$ ls -a
.   .bash_history  .bashrc  .config  .kshrc  .locallogin  .modulesbegenv  .procmailrc  .ssh       .zshenv  hello.txt
..  .bash_profile  .cache   .cshrc   .local  .login       .motd           .profile     .zprofile  .zshrc   perl5

[cs15lfa22bh@ieng6-203]:~:18$ ls -lat
total 116
-rw-r--r--   1 cs15lfa22bh ieng6_cs15lfa22  1318 Oct 13 09:18 .modulesbegenv
-rw-r-----   1 cs15lfa22bh ieng6_cs15lfa22    30 Oct 12 22:50 hello.txt
drwxr-s---   7 cs15lfa22bh ieng6_cs15lfa22  4096 Oct 12 22:50 .
-rw-r-----   1 cs15lfa22bh ieng6_cs15lfa22     0 Oct 12 22:32 .motd
drwxr-sr-x 467 cs15lfa22   ieng6_cs15lfa22 36864 Oct  6 08:06 ..
-rw-------   1 cs15lfa22bh ieng6_cs15lfa22   389 Oct  5 16:05 .bash_history
drwx--S---   2 cs15lfa22bh ieng6_cs15lfa22  4096 Oct  5 14:51 .ssh
drwxr-sr-x   2 cs15lfa22bh ieng6_cs15lfa22  4096 Oct  5 14:20 perl5
drwxr-sr-x   3 cs15lfa22bh ieng6_cs15lfa22  4096 Oct  5 14:20 .local
drwxr-sr-x   3 cs15lfa22bh ieng6_cs15lfa22  4096 Oct  5 14:20 .config
drwxr-sr-x   3 cs15lfa22bh ieng6_cs15lfa22  4096 Oct  5 14:20 .cache
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22   290 Sep  8 16:11 .zshrc
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22   481 Sep  8 16:11 .zshenv
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22  1931 Sep  8 16:11 .zprofile
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22  1961 Sep  8 16:11 .profile
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22   837 Sep  8 16:11 .procmailrc
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22   431 Sep  8 16:11 .login
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22   155 Sep  8 16:11 .locallogin
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22  1692 Sep  8 16:11 .kshrc
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22  1931 Sep  8 16:11 .cshrc
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22  1721 Sep  8 16:11 .bashrc
-rwxr-x---   1 cs15lfa22bh ieng6_cs15lfa22   975 Sep  8 16:11 .bash_profile

[cs15lfa22bh@ieng6-202]:~:21$ ls /home/linux/ieng6/cs15lfa22/cs15lfa22bh
hello.txt  perl5
```
```ls``` shows all the non-hidden files in the current directory, whereas ```ls -a``` shows all of the files, hidden & non-hidden, in the current directory, & ```ls -lat``` presents a more detailed look into the directory's hidden & non-hidden files. ```ls <directory>``` shows the files in that particular directory.
```
[cs15lfa22bh@ieng6-202]:~:22$ cp /home/linux/ieng6/cs15lfa22/public/hello.txt ~/
```
`cp` copies a file from the path set in the first argument to the second argument. In this case, `hello.txt` is being copied to the home directory.
```
[cs15lfa22bh@ieng6-202]:~:23$ cat /home/linux/ieng6/cs15lfa22/public/hello.txt
Hi! Welcome to CSE15L Fall 22
```
`cat` is used to display the contents of the file on the terminal.
## Moving Files with ```scp```
Before proceeding to experiment with scp, first we need to make a new file on our computer called ```WhereAmI.java``` with the contents below.
```
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}
```
As a reference, this is what mine looks like:

![Image](/images/whereami%20file.jpg)

I've already tried compiling the program myself in the terminal, but the program essentially prints out information about the current computer and user information that I am using.

In the same terminal, I used the scp command to copy the file from the client (my personal computer) to the server (ieng6 computer). This change can be seen when we look into the directory on the server. The ```WhereAmI.java``` can now be run through the server terminal.
```
// this is before copying WhereAmI.java to the server
[cs15lfa22bh@ieng6-202]:~:24$ javac WhereAmI.java
javac: file not found: WhereAmI.java
Usage: javac <options> <source files>
use -help for a list of possible options

// using scp to copy the file to the server
PS C:\Users\justi> scp WhereAmI.java cs15lfa22bh@ieng6.ucsd.edu:~/  
Password: 
WhereAmI.java 

// checking that WhereAmI.java jas been copied over
[cs15lfa22bh@ieng6-202]:~:25$ ls
WhereAmI.java  hello.txt  perl5

// trying out WhereAmI.java on the server
[cs15lfa22bh@ieng6-202]:~:26$ javac WhereAmI.java
[cs15lfa22bh@ieng6-202]:~:28$ java WhereAmI     
Linux
cs15lfa22bh
/home/linux/ieng6/cs15lfa22/cs15lfa22bh
/home/linux/ieng6/cs15lfa22/cs15lfa22bh
```
## Setting an SSH Key

In order to make the logging in process quicker when trying to perform tasks with the remote computer, SSH keys can be used to minimize this. To begin setting an SSH key, enter the following command into your **client** terminal:
```
PS C:\Users\justi> ssh-keygen
```
Once you enter this into the terminal, you should be prompted to enter a file to save the key, and you can press enter here to save it at the default location given. For a reference, this is what the process looked like on my end.

![Image](/images/ssh%20keygen.jpg)

Since I'm currently on a Windows, I've followed an additional step for doing `ssh-add`. After generating the SSH key, I entered the following commands into my terminal as an administrator:
```
PS C:\WINDOWS\system32> Get-Service ssh-agent | Set-Service -StartupType Automatic
PS C:\WINDOWS\system32> Start-Service ssh-agent
PS C:\WINDOWS\system32> Get-Service ssh-agent

Status   Name               DisplayName
------   ----               -----------
Running  ssh-agent          OpenSSH Authentication Agent


PS C:\WINDOWS\system32> ssh-add  C:\Users\justi/.ssh/id_rsa
Identity added: C:\Users\justi/.ssh/id_rsa (justi@LAPTOP-GTF412KS)
```
Now logging back into the server, enter the following command and then log back out.
```
[cs15lfa22bh@ieng6-202]:~:21$ mkdir .ssh
mkdir: cannot create directory '.ssh': File exists
[cs15lfa22bh@ieng6-202]:~:22$ logout
Connection to ieng6.ucsd.edu closed.
```
Back on the client side, enter the following command. Now I should be able to use `ssh` & `scp` without having to enter my password again from this device. 
```
PS C:\Users\justi> scp /Users/justi/.ssh/id_rsa.pub cs15lfa22bh@ieng6.ucsd.edu:~/.ssh/authorized_keys
Password: 
id_rsa.pub                                                  100%  576    70.1KB/s   00:00 
```
## Optimizing Remote Running

Now that we've set up an SSH key, it should be less tedious trying to work with the server. Below are some commands that I've tried running to see how efficient the process has become.
```
PS C:\Users\justi\Documents\GitHub\cse15l-lab-report> ssh cs15lfa22bh@ieng6.ucsd.edu "cat WhereAmI.java"
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}

PS C:\Users\justi\Documents\GitHub\cse15l-lab-report> ssh cs15lfa22bh@ieng6.ucsd.edu "cat hello.txt WhereAmI.java"
Hi! Welcome to CSE15L Fall 22
class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}

PS C:\Users\justi\Documents\GitHub\cse15l-lab-report> ssh cs15lfa22bh@ieng6.ucsd.edu ls                                                                              WhereAmI.class
WhereAmI.java
hello.txt
perl5

PS C:\Users\justi\Documents\GitHub\cse15l-lab-report> ssh cs15lfa22bh@ieng6.ucsd.edu "cd ~; ls -a"
.
..
.bash_history
.bash_profile
.bashrc
.cache
.config
.cshrc
.kshrc
.local
.locallogin
.login
.modulesbegenv
.motd
.procmailrc
.profile
.ssh
.zprofile
.zshenv
.zshrc
WhereAmI.class
WhereAmI.java
hello.txt
perl5
