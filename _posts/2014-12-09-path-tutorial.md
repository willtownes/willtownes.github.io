---
title: Installing Command Line Utilities on Mac OS X
layout: post
comments: true
---

This is an overview of different options for installing command line utilities on Mac OS X. The focus of the example is the program [Plink](http://pngu.mgh.harvard.edu/~purcell/plink/download.shtml) which is used for processing genomics data. But the concepts would apply to any command line tool.

### Command Line Crash Course
If you don't know anything about using the command line, check out Zed Shaw's tutorial [Learn Command Line the Hard Way](http://cli.learncodethehardway.org/book/). It has a lot of good exercises and can serve as a reference if you forget which command to use. Refer to this site if you are confused by any of the commands required by the instructions below.

### Scenario I: I will use command line frequently
If you will be using other command line tools other than just plink, and/or if you anticipate needing to frequently update your command line tools to newer versions over time, then [Homebrew](http://brew.sh/) is an integrated solution. Go to the Homebrew site and follow their instructions for installing the homebrew package manager. Once this is completed, go to the terminal and type the following to install Plink

{% highlight bash %}

    brew tap homebrew/science
brew install plink

{% endhighlight %}

Homebrew/science is a "tap", meaning it contains specialized packages (also known as "formulas") related to science not found in the default, mainstream Homebrew repository. You can read more about it on the github repository [Homebrew/science](https://github.com/Homebrew/homebrew-science/blob/master/README.md)

### Scenario II: I will use command line rarely
This option is the quickest, easiest way to get plink working on mac, but it may cause you frustrations over time since it won't facilitate updating to newer versions in the future. Avoid this approach if you will be using more than one command line utility and/or make frequent use of command line tools in the future.

1. Go to the [plink website](http://pngu.mgh.harvard.edu/~purcell/plink/download.shtml) and download the latest version of the software.
2. Unzip the downloaded file. Usually you can just double click on it. 
3. Let's say for example the zip file was expanded to the folder `/Users/MYNAME/Downloads/plink-1.07-mac-intel`. Whatever this folder name is on your machine, open it in the finder and check to make sure it contains the executable file `plink`. Then open the terminal and navigate to that folder with the command
    
    ``cd /Users/MYNAME/Downloads/plink-1.07-mac-intel``

4. We are going to copy the `plink` executable into a folder that is in the system's **PATH** variable. There are ways to modify the **PATH** variable such as by altering the file `~/.bash_profile`. However, this method just uses the default **PATH** for simplicity. Run the following command
    
    ``cp plink /usr/local/bin/plink``

    If you get an error about permissions, try this instead (it will ask for your password):

    ``sudo cp plink /usr/local/bin/plink``


5. Now close the terminal and a new terminal window in an arbitrary directory. Type `plink` and hit enter to see if the computer will run the program as expected.





























