# CSE 15L Week 1 Lab Report

In this lab report we will be discussing how to access and editing files on a remote machine through the ssh and scp terminal commands. My personal machine runs Ubuntu so that will be the perspective from which I will write this guide.

## Step 1: Installing VSCode

Our first step is to install Visual Studio Code onto our machine. All you need to do is visit [the visual studio code website](https://code.visualstudio.com/download) and click the large download button labeled `.deb`.

![step1.1](https://ethan-talbert.github.io/cse15l-lab-reports/images/week-1/week1-step1.1.png)

After downloading the `.deb` file, navigate your terminal to the location of the downloaded file and run the command:

`sudo apt install FILE_NAME_HERE.deb`

This should install VSCode onto your computer, completing the first step.

## Step 2: Remotely Connecting

Once you have VSCode, connecting to a remote machine using the ssh command is very easy. Simply click the 'Terminal' button at the top of the VSCode window and type in the following command:

`ssh cs15lfa22hj@ieng6.ucsd.edu`

The part before the @ symbol represents your username for this class and can be changed out if you have a different username. The part after the @ symbol represents the remote machine you are connecting to. After you type in the command it should ask for a password. Type in your password for this account and press enter. If all goes well you should have an output like this:

![step2.1](https://ethan-talbert.github.io/cse15l-lab-reports/images/week-1/week1-step2.1.png)

## Step 3: Navigating the Remote Machine

Once we have connected to the remote machine, we can have some fun with it. Here are a couple commands as well as what they do:

`cd <filepath>` - Changes the directory to what is given as an argument

`ls` - Lists all files and directory within the current directory

`mkdir <directory name>` - Creates a new directory in the current directory

Here is an example of me navigating through the remote machine using these commands:

![step3.1](https://ethan-talbert.github.io/cse15l-lab-reports/images/week-1/week1-step3.1.png)

Try them out for yourself a little bit before we continue here just to get used to working on a remote machine. Once you are finished, use the `exit` command to get back to your local computer.

## Step 4: Moving Files Using `scp`

In order to get the most use out of remote machines, we need to be able to move data and code from our own computers to the remote one. For this step we'll be using the `WhereAmI.java` program we've used in the past. Add a java file with this code in it to your local machine:

![step4.1](https://ethan-talbert.github.io/cse15l-lab-reports/images/week-1/week1-step4.1.png)

When we compile and run this file on our own personal computer, we get something like the following:

![step4.2](https://ethan-talbert.github.io/cse15l-lab-reports/images/week-1/week1-step4.2.png)

Now let's try and copy this file to our remote machine. Type in the following command and type your password when it prompts you.

`scp WhereAmI.java cs15lfa22hj@ieng6.ucsd.edu:~/`

This will copy the file over to the remote machine. Now, once we `ssh` back into the machine, we can compile and run it there and we will get something like this:

![step4.3](https://ethan-talbert.github.io/cse15l-lab-reports/images/week-1/week1-step4.3.png)

This means that our program is running from inside the remote machine, and that we successfully copied code from our local machine to the remote one.

## Step 5: Setting an ssh key

Typing in a password every time you want to get into the remote machine seems inefficient. Luckily there's an easy way to circumvent this: by setting an ssh key. Run `ssh-keygen` in your terminal and press enter through all of the prompts. You should get something similar to this:

![step5.1](https://ethan-talbert.github.io/cse15l-lab-reports/images/week-1/week1-step5.1.png)

Once you have generated your ssh keys, you need to move to public one to the remote machine. Let's first make a folder for ssh keys in our remote machine. Connect to the machine and make a directory named `.ssh`. Now, exit back to your local machine and run the following command:

`scp ~/.ssh/id_rsa.pub cs15lfa22hj@ieng6.ucsd.edu:~/.ssh/authorized_keys`

If all went well, you now should be able to ssh into the remote machine and scp files without inputting a password.