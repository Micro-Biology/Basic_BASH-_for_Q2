# Basic_BASH_for_Q2

In this tutorial I will cover basic BASH commands for use in comand line interface (CLI) to complement the use of Qiime2. This will be from the perspective of an Ubuntu user but should cover most if not all Linux distrubutions (and probably MacOS with a little tweaking). If you are a novice CLI user I advise running through this tutorial and learning.

In linux we use the 'cd' command for example:

    cd ~ #this will direct us to your home directory
    
    cd ~/QiimeScripts #this will direct us to the folder QiimeScripts in the home directory no matter where we currently are
    cd QiimeScripts #this will direct us to the folder QiimeScripts that is contained within the current target directory 
    
To go up one in the folder heirachy use:

    cd ..
    
For example assuming you opened a terminal and ran these scripts you would first be taken to the home directory (~), then to ~/QiimeScripts, and then to ~/QiimeScripts/~/QiimeScripts, and then back to ~/QiimeScripts.

But wait you're saying you got an error when running 'cd ~/QiimeScripts' !!!

    bash: cd: /home/nls/QiimeScripts: No such file or directory

This is because you don't have a directory ~/QiimeScripts, lets make one using the 'mkdir' command:

    mkdir QiimeScripts
    
And if you need to make a chain of folders:

    mkdir -p ~/QiimeScripts/folders/that/dont/exist/yet
    
Oh no we didnt actually want all those folders there lets remove all the folders within QiimeScripts using 'rm'

    rm ~/QiimeScripts/folders

Uh, not another error!

    rm: cannot remove '/home/nls/QiimeScripts/folders': Is a directory
    
This is because rm can only be used on files...
... I lied you can remove directories using 'rm -r' but be careful it will delete everything in those folders and they will not go to the recycling bin.

    rm -r ~/QiimeScripts/folders
    
Lets install an application that means are items can be sent to the recycling bin more easily:

    sudo apt-get install trash-cli
    
Okay now we just use 'trash' instead of 'rm':

    trash ~/QiimeScripts
    
Oh no you're telling me you had important scripts and data in that folder!?
Just as well we used 'trash' and not 'rm':

There are other CLI based trash applications such as trash-restore ect, but for now just restore the files using the GUI.

Right now lets navigate back to our folder:

    cd ~/QiimeScripts
    
To see all the files you just almost lost use the 'ls' command, and alternative is the 'dir' command, its not quite as informative, try them both:

    dir
    ls
        
These commands will give you a list of all the files within current directory and an be a very powerful tool.
Alternatively you can use it on another directory eg:

    ls ~/
    
These are all the files and directories contained directly within the home directory.
