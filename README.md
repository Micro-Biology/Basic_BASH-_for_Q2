# Basic BASH for Q2

In this tutorial I will cover basic BASH commands for use in comand line interface (CLI) to complement the use of Qiime2. This will be from the perspective of an Ubuntu user but should cover most if not all Linux distrubutions (and probably MacOS with a little tweaking). If you are a novice CLI user I advise running through this tutorial and learning.

## Folder navigation, and moving files

In linux we use the 'cd' command for example:

this will direct us to your home directory:

    cd ~
    
This will direct us to the folder QiimeScripts in the home directory no matter where we currently are:
    
    cd ~/QiimeScripts
    
his will direct us to the folder QiimeScripts that is contained within the current target directory:
    
    cd QiimeScripts 
    
To go up one in the folder heirachy use:

    cd ..
    
For example assuming you opened a terminal and ran these scripts you would first be taken to the home directory, then to 'QiimeScripts', and then to 'QiimeScripts/QiimeScripts', and then back to 'QiimeScripts'.

But wait you're saying you got an error when running 'cd ~/QiimeScripts':

    bash: cd: /home/nls/QiimeScripts: No such file or directory

This is because you don't have a directory ~/QiimeScripts, lets make one using the 'mkdir' command:

    mkdir QiimeScripts
    
And if you need to make a chain of folders:

    mkdir -p ~/QiimeScripts/folders/that/dont/exist/yet
    
Oh no we didnt actually want all those folders there lets remove all the folders within QiimeScripts using 'rm':

    rm ~/QiimeScripts/folders

Uh, not another error!:

    rm: cannot remove '/home/nls/QiimeScripts/folders': Is a directory
    
This is because rm can only be used on files...

... I lied you can remove directories using 'rm -r' but be careful it will delete everything in those folders and they will not go to the recycling bin.

    rm -r ~/QiimeScripts/folders
    
Lets install an application that means are items can be sent to the recycling bin more easily:
(WARNING: This will not work for MacOS, you can either use the program [here](https://github.com/morgant/tools-osx), you may also want to conser using [homebrew](https://brew.sh/), which can be used to install instead of 'apt-get'. I don't know how MacOS works so if anyone would like to help em out here that would be great!)

    sudo apt-get install trash-cli
    
Okay now we just use 'trash' instead of 'rm':

    trash ~/QiimeScripts
    
Oh no you're telling me you had important scripts and data in that folder!?
Just as well we used 'trash' and not 'rm':

There are other CLI based trash applications such as trash-restore ect, but for now just restore the files using the GUI.

Right now you've restored the folder lets navigate back to our folder:

    cd ~/QiimeScripts
    
To see all the files you just almost lost use the 'ls' command, and alternative is the 'dir' command, its not quite as informative, try them both:

    dir
    ls
        
These commands will give you a list of all the files within current directory and an be a very powerful tool.
Alternatively you can use it on another directory eg:

    ls ~/
    
  
These are all the files and directories contained directly within the home directory.

Right so lets run some qiime 2 scripts, but wait first we need to get the data from '~/Data'. ~~I'll just copy and paste it over~~

No, we're CLI for life now!

    ~/Data
    dir
    
Thats a lot of files... okay I know we can use the * to mean any characters, lets try:

    cp ~/Data/*.fastq.gz ~/QiimeScripts
    
Wow, that was even easier than Ctrl-C Ctrl-V! 

Oh no I meant to move them into a folder Analysis within QiimeScripts, lets use the 'mv' command:

    cd QiimeScripts
    mkdir Analysis
    mv *.fastq.gz Analysis/
    
You are now ready to start learning Qiime 2! Start here https://docs.qiime2.org/2018.8/tutorials/ If you get stuck with CLI issues come back here.
    
## Shell scripts

Great now we can run some qiime 2 scripts, but wouldn't it be good if we didn't have to type them out or copy and paste them everytime...?

Where there is a will there is a way, enter the Shell script.

First make a new document, and open it in an editor (I'll use gedit):

    touch Q2_Analysis.sh
    gedit Q2_Analysis.sh
    
First we have to put what is known as a shebang line, this is my prefered line below:

    #!/bin/bash
    set -e
    set -u 

The first line tells the terminal this is a BASH script, the second line tell the script to halt if there are any errors, and the final line stops the script if there are any unset variables.

Then add your Qiime 2 pipeline that you want to be repeatable, you may want to just do each step in its own script or you may like to do the entire pipeline from start to finish, its up to you.

To make the script executable first, run:

    sudo chmod 755 Q2_Analysis.sh 
    
And then simply:

    ./Q2_Analysis.sh
    
## Trouble shooting
    
You will probably get some sort of errors, make sure your directories are called correctly, and that file names match. Most/any of the scripts in this tutorial will work when using shell scripts, so knock yourself out. Additonally ther is one more command I find very useful for working out where in your pipeline you are up to, echo:

    echo "Hello World!"
    echo "Copying files to Analysis folder"
    echo "Backing up raw data files"

## Final word

Well if you got this far, well done! You are ready to start using the CLI to make impress all your coworkers and friends (okay maybe not!). If you need any more help I advise googling any problems you have, and reading the manuals for each command if you need it to work slightly differently, the BASH manual can be found here: https://ss64.com/bash/

Good luck!
