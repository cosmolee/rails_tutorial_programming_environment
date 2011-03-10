# *Ruby on Rails 3 Tutorial* environment setup instructions

These instructions will produce the full development environment as described in the book with Ruby 1.9.2 and ROR 3.  It is complete with the optional RVM - Ruby Version Manager, Growl - pop-up notifications, Inotify - file system monitor (like FSevent for Mac OSX), SQLite Database Browser, and Autotest - automated continuous testing, running with Spork for fast test runs.  These instructions can also be used as a template to quickly get up and running with a useful development environment for your own projects.  

I use version 10.04 of Ubuntu Linux as the base platform because it is an LTS (Long Term Support) release which will have maintenance support for an extended period.  Most significant problems that cause things to break (and much hair pulling) are in the Ruby Gems interactions.  This is taken care of by the supplied Gemfile, which specifies the particular set of gems required to create a functioning gemset for our purposes.  Since the gems interaction problem has been taken care of here, if you are already using a different version (Ubuntu 10.10 & Linux Mint 10 also work) of Ubuntu (or Ubuntu-based distro), the instructions will most likely work for you as well, with, perhaps, minor modifications.  

If you wish to use the Linux environment for more than the development purposes here, say, playing movies from DVD, browse sites with Flash content, or as a general desktop, see below for a link to Mint Linux 10, which is an Ubuntu-based distro.  It's a friendlier Linux experience than Ubuntu, and comes pre-installed with codecs for playing DVDs, MP3, Flash, etc. It generally makes it easier to access content that uses proprietary content.   

I've tested the instructions extensively by starting from scratch Ubuntu installs and executing the instructions line by line.  You may be able to get the environment set up on an existing Ubuntu installation.  Worst-case, if you start with a clean install of Ubuntu 10.04, perhaps on a separate drive partition or a virtual machine, and follow these instructions exactly, you will have a functional "ROR 3 Tutorial" environment.  This just works.

You still have to do the configuration per the book for GIT and Heroku (Chap. 1), but the required software to do the exercises will already be installed, and the resulting programming environment is very nice to work with.  I tried to install all the software required for the exercises, but as of this writing, I still have not yet gotten past Chapter 3, since all the problems that I encountered side-tracked me into this project.  Please let me know if I've left anything out or if you have any problems I should know about...

If you have any comments or issues, please post to the GetSatisfaction thread, where there are likely to be more eyes viewing this topic:  

http://getsatisfaction.com/railstutorial/topics/set_up_rails_tutorial_programming_environment_instructions_linux_windows


There is a sister project which provides a fully complete bootable development environment that has all these steps already done, which can be run from a flash drive, CD, or virtual machine.  Just plug in a flash drive and boot.  None of the installation or configuration business required.  If that appeals to you, you can find it here:

http://getsatisfaction.com/railstutorial/topics/rails_tutorial_programming_environment_ready_bake_version_linux_win_or_mac

-Cosmo Lee



## Windows installation notes

If you are a Windows user having problems setting up a satisfactory ROR environment, or are simply looking for an easy setup, you can load Ubuntu with the "Windows Ubuntu Installer" - WUBI. This allows you to install Ubuntu "inside" Windows like a regular application, without the involvement of having to create a separate disk partition.  With these instructions, you probably have a solution with less friction than trying to load the environment natively and having to figure out all the dependencies on your own.  

Note: The Windows Installer option has been known to have issues booting Linux if you have multiple operating systems installed on various partitions on your hard drive.  If you only have Windows installed on your drive, you'll probably be OK.  YMMV.  But it's pretty painless to give it a try and see if it will work for you.  If it doesn't work, you simply uninstall Ubuntu from your Windows application programs.  If you can't get the Ubuntu "inside" Windows option to work, you still have as a fall back the option of installing Ubuntu to a separate partition on your hard drive.  

To install to a separate partition, install Ubuntu from a DVD and the install process will walk you through creating a new partition.  If you haven't already installed Windows, but are planning on running both Windows and Linux together on the same hard drive in separate respective partitions, you should install Windows first.  Windows has been known to not play nice with other operating systems and blow away the ability to boot the other operating system upon a new install.  

Since these options are based on Open Source software, they cost you nothing to try.  

Note: the lines below that start with the "$" sign are commands that are to be executed at the command line from a terminal.  The "$" sign is analogous to the DOS "C:>" prompt; you don't actually type "$" when you execute the commands.  If you see the "#" character, it and the following text are comments, so don't include that as part of the command.  

So if you see:

    $ echo howdy    #Echo the word howdy

You only actually type at the command line:

    echo howdy


## Linux Download Links

http://linuxmint.com/
Linux Mint 10 also has an "inside" Windows install option.  To access that, boot from the installation DVD.

https://wiki.ubuntu.com/WubiGuide
http://www.ubuntu.com/desktop




# LET'S BEGIN...


# INSTALL REQUIRED LINUX SOFTWARE

Open a terminal.  From the system menu, click Applications -> Accessories -> Terminal

Update package list:

    $ sudo apt-get update


Install various required Linux packages:

    $ sudo apt-get install zlib1g zlib1g-dev libssl-dev build-essential sqlite3 libsqlite3-dev sqlite3-doc git-core curl libxslt1-dev libxml2-dev  git-core libreadline6 libreadline6-dev libyaml-dev libsqlite3-0 autoconf libc6-dev bison openssl libnotify-bin vim emacs sqlitebrowser



## INSTALL RVM & RUBY

    $ bash < <( curl http://rvm.beginrescueend.com/releases/rvm-install-head )



* Get .bashrc file from GIT repository.  Make edits to .bashrc file.  


Edit the RVM config lines in .bashrc.  See README file in .rvm directory for more info.  I find the instructions there to be cumbersome.  I simply put the required line at the top of the .bashrc file to achieve the same thing, instead of changing the logic of the code as suggested by the RVM README file.  This worked fine for me with a stock .bashrc file.  If this doesn't work for you, you can follow those instructions instead.  If you haven't made any changes to your .bashrc file, you can just grab the entire file from the GIT repository and overwrite/create your .bashrc with it.  These are the .bashrc file edits I made.  Add your own .bashrc changes, if any.

Note to Windows users: to edit files you can run the included text editor.  Click on the System menu icon, click Accessories -> Text Editor  Choose/create the file in your home directory named ".bashrc".  Or downloaded the file from the GIT repository and copy to your home directory.


This loads RVM into shell sessions, added:

    # This loads RVM into shell sessions.
    [[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm"  


When you start using multiple gemsets, it's easy to lose track of which gemset you're currently using and make mistakes, thinking you're using a different gemset, resulting in unexpected and confusing behavior.  So I've made a change to the shell prompt to always show the current RVM gemset, added:

    #Add RVM gemset name
    PS1="\$(~/.rvm/bin/rvm-prompt) $PS1"



*QUIT* terminal and open a new terminal, you should now be running the new environment.  Confirm RVM loaded correctly:

    $ type rvm | head -1

Should result in this output: 

    rvm is a function



Install Ruby 1.9.2:

    $ rvm package install zlib
    $ rvm install 1.9.2 


Create gemset for tutorial use:

    $ rvm --create use 1.9.2@rails3tutorial


Make that gemset the default

    $ rvm --default use 1.9.2@rails3tutorial


Your command prompt should now be showing the current gemset.  Something like:

    ruby-1.9.2-p136@rails3tutorial login-name@computer-name:~$



## INSTALL RAILS 3


    $ gem install rails --version 3.0.3 


Make a directory for your Rails projects:

    $ mkdir rails_projects  
    $ cd rails_projects



## Create Rails app (Chap 3)

This is the first exercise in the book in Chapter 3.  Here we set up the environment that you'll be using for the main book project.  When you later follow along in the book and come to this chapter, *remember that you've already done this*.  Otherwise, you'll blow away the work you're about to do and will have to re-do these steps.  So DON'T repeat the following commands.  You might want to write a sticky note and place it in the book or on your screen so you won't forget.  If you do forget and try to re-create the project, Rails will give you an Overwrite warning that you are about to do so.  If so, type "q" at the prompt to exit the process.

    $ rails new sample_app -T
    $ cd sample_app



## SET UP PROJECT GEMS

* Create Gemfile with specific dependencies and versions.  Replace sample_app/Gemfile with file from GIT repository.



Create bundle for project:

    $ bundle install

    ...

    Your bundle is complete! Use `bundle show [gemname]` to see where a bundled gem is installed.



## SET UP RSPEC

You might see an error message generated: "Could not find "autotest" in any of your source paths."
Ignore, since `type autotest` does show autotest in PATH.

    $ rails generate rspec:install


* Edit sample_app/.rspec file in Rails project root directory.  Replace that with repository file.



This is an exercise in the book, chap 3.  We'll run it to test that we've got functionality:
    
    $ rails generate controller Pages home contact


You should be able to run rspec tests successfully:

    $ cd ~/rails_projects/sample_app    #Change to project root directory before running rspec
    $ rspec spec/                #Ignore the "No DRb server" warning
    
    ...

    Finished in 0.28896 seconds
    5 examples, 0 failures, 3 pending



# SET UP SPORK

Set up Spork:

    $ spork --bootstrap


* Edit sample_app/spec/spec_helper.rb file per listing 3.12.  Replace that with repository file.


* Edit sample_app/config/application.rb per listing 3.13.  Replace that with repository file.  Note: if you are using this file for other then sample_app, you must change the module name in the file to reflect the project name.




We're ready to see the improved runtime of our tests.  Get a baseline on test time:

    $ cd ~/rails_projects/sample_app    #Change to project root directory before running rspec
    $ time rspec spec/            #Ignore the "No DRb server" warning

Open up *another* terminal tab <shift+ctrl+T> and run Spork.  

    $ spork

    ...

    Loading Spork.prefork block...
    Spork is ready and listening on 8989!
       


After you see the "Spork is ready and listening" message, switch back to the previous terminal tab to run fast tests. Note difference in test times.  Much faster!  

    $ time rspec spec/





# SET UP AUTOTEST

Create sample_app/.autotest file.  Replace that with repository file.

You may now run autotest (Chap 3).  You will see some errors about variables (see notes below), but autotest runs fine.  Be sure that you are in the project root directory.

    $ cd ~/rails_projects/sample_app    #Change to project root directory before running 
    $ autotest

    ...

    Finished in 0.26421 seconds
    5 examples, 0 failures, 3 pending

    # Waiting since 2011-01-22 21:34:59



Autotest will do an initial run of your tests, when it finishes, you will see a Growl notification of the test run.

If you go to another terminal screen and edit a monitored file in the project, then save it, you will then see a Growl notification that autotest has detected a file change and is running the tests automatically. Try just adding a trivial extra space to sample_app/app/controllers/pages_controller.rb, then saving it.  You should see a notification pop up when you save the file.  If you switch to the terminal tab where you ran autotest, you will see that it is running the rspec tests for that file.


SWEET! DONE!!



## BUG NOTICES

* Autotest will not exit with <ctl-c> <ctl-c> (twice) as is normal.  This is a bug caused by autotest-inotify.  The fix is to cause some activity in the project file hierarchy (which autotest-inotify is watching).  Open or go to another terminal screen and do an `ls` on a directory in the same project file hierarchy, then autotest will exit.  If you don't like this, remove the "require autotest/inotify" line in the ".autotest" file to get rid of inotify functionality.  This issue shouldn't really have any impact on you as normally you wouldn't have a reason to manually exit autotest.  There seems to be some bugginess with inotify blocking autotest.

* Be sure that when you run the autotest command that you are in the project root directory.  If you are somewhere else, it may just sit there telling you nothing useful.


* Not actually a bug, but Spork pre-loads some files in order to run tests fast.  But if you make changes to these files, they won't be noticed.  If you find that you keep getting an error from the tests, but you are sure that your code was correct, you may be editing a pre-loaded file.  

An example of this happens in exercise 3.18.  You are instructed to edit config/routes.rb and app/controller/pages_controller.rb.  However, when the tests run, an error gets thrown saying there isn't a route to controller: page, action:about.  This is because Spork did not register the change to routes.rb because it was preloaded.  In order to have this register you must kill and restart Spork.  

To see which files Spork pre-loads, run `spork --diagnose`


## INSTALLATION NOTES

You may see various warnings when running autotest with autotest-inotify, however, it appears to run fine despite them.  If you don't like this, remove the "require autotest/inotify" line in the .autotest file to get rid of inotify functionality.  However, without inotify your drive will have to continually manually check for changed files, instead of being automatically notified by the file system monitor.  


    $ autotest
    loading autotest/rails_rspec2



If there is a warning about no DRB server running, then you are not already running `spork` prior to running the tests.  In such a case, your tests will still run, but without the speed benefits of Spork:

    No DRb server is running. Running in local process instead ...

*See "Usage-Notes.txt" file for further info on using the environment.*

