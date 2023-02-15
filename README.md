# GitHub-WSL-Tutorial
*Authors: [Eric Udlis](http://ericudlis.com), Ben Everson, Noah Kurszewski, [James Vollmer](https://jrvollmer.github.io)*

This tutorial is to provide instructions on the installation and setup of WSL and GitHub and to introduce version control using GitHub.

This Tutorial is based on the one from [hubspot](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners)

# WSL and Ubuntu Installation and Setup (Fellow Windows People Start Here)
This portion of the tutorial is to guide new Firmware members in the installation of WSL. Requirements for this tutorial are that you are using your **personal laptop** that runs **Windows 10, Windows 11, or Linux**. Windows users, please complete WSL installation before continuing with the GitHub tutorial. If you use Linux, then you can skip ahead to the GitHub portion.

## Step 0: Install Windows Terminal
I have found that Windows Terminal works best for WSL, as it combines PowerShell and your WSL distribution into one terminal. If your laptop doesn't already have it installed, you can download it [here](https://www.microsoft.com/store/productId/9N0DX20HK701).

### Open Windows Terminal
After it installs, open Windows terminal as an administrator by right clicking on the Terminal icon, then clicking "Run as adminstrator." Your terminal will likely initially open to Command Prompt or PowerShell. If it doesn't open to PowerShell, click the dropdown arrow to the right of the plus button and select Windows PowerShell.

## Step 1: Install WSL

Once running PowerShell as an admin, type ```wsl --install``` in the terminal and hit enter. If all goes to plan, WSL will begin installing Ubuntu, and the terminal window will begin outputing its progress. Once the installation finishes, the terminal will tell you that a restart is required. Restart your computer now, then return to the tutorial.

Once you're back, open Terminal as an admin again, open PowerShell and run the following command: ```wsl --set-default-version 2```. This sets your WSL to the correct version for our use.

[Install link](https://learn.microsoft.com/en-us/windows/wsl/install)

## Step 2: Ubuntu Setup

After the restart, an Ubuntu window should open automatically and display the progress of the last of the Ubuntu installation. If it didn't open, use the Start menu or the Windows search bar to search for Ubuntu. It will appear as a Windows application, so open it up like you would any other app. After the installation finishes, you will be asked to enter in a username and password for your distribution. You can choose whatever you'd like for these, but an important thing to note is that you will not be able to see your password as you type. This is a security feature called blind typing, and is completely normaL.

As you likely noticed, the Ubuntu window did not open in Windows Terminal. Once you've set your login, close out the window and pull up Windows Terminal. To get to Ubuntu in Terminal, click the dropdown arrow to the right of the plus button, then click on Ubuntu.

Now in the Ubuntu terminal, type ```cd ~``` to ensure you're in your root directory. Next, run ```sudo apt update && sudo apt upgrade``` to ensure all of your packages are up to date. 

# GitHub Tutorial

## Step 0: Install Git

### Ubuntu

Open Ubuntu in Windows Terminal by clicking the dropdown arrow to the right of the plus button, then click on Ubuntu. Once in the linux terminal, run the following command to ensure git is installed.

```
sudo apt install git
```

### Windows

Download git [here](https://git-scm.com/downloads). Follow the walkthrough, all default options should be good. Don't touch them unless you know what you're doing.

## Step 0 (Continued): Set up GitHub SSH Key

 1. Follow the instructions in the “Generating a new SSH key” section of [Generating a new SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent). It isn’t necessary to add your SSH key to the ssh-agent.
 2. Follow the instructions on [Adding the SSH key to your GitHub account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account).
    - When you copy your SSH key to GitHub, it should have your email at the end of it.

## Step 0 (Almost There): Configure Your Git User Settings

```
Bucky@Badgerloop~$: git config --global user.name "<Your name>"                                                 // Sets the name Git associates with you
Bucky@Badgerloop~$: git config --global user.email "<The email that you used to set up your GitHub account>"    // Sets the email Git associates with you
Bucky@Badgerloop~$: git config --global --list                                                                  // Lists your Git profile information
user.email=bbadger@wisc.edu
user.name=Bucky Badger
... Maybe some other stuff if you've added other info
```

## Step 1: Clone the Repository
No matter what project you're working on in Badgerloop, you will always be working in a repository (Repo for short). To use git we'll be using the terminal. Check out some tutorials on the wiki. In this guide you will need to know the following.
```
Bucky@Badgerloop~$: ls    // Lists the files and directories in your current directory
Bucky@Badgerloop~$: cd    // Navigates to directory use `cd ..` to navigate up a directory
Bucky@Badgerloop~$: pwd   // Prints your working directory
```
We already have code up on GitHub so the first step is to "clone" a copy of what we have on your local machine. To begin, open up a terminal (on windows use Git Bash or WSL to follow the commands used in this tutorial) and navigate to where you'd like your project to be located. If you have a "projects" folder, this would be the place. This command will navigate you to your home directory
```
Bucky@Badgerloop~$: cd ~ 
```
Next grab the clone link from the GitHub Page. You will need to navigate to the actual webpage of the git repository on GitHub. You can find a list of all Badgerloop Repos by [clicking here](https://github.com/badgerloop-software/). If you're reading this on the GitHub page, just click the green button in the upper right that says "Code." This opens a dropdown window. In that window, click "SSH" if it isn't already selected, then copy the link to your clipboard. We'll need it in the next step.

Finally, execute a git clone command to copy the repository to your local machine by typing
```
Bucky@Badgerloop~$: git clone gitLinkHere
```
This will create a directory with the most up to date version of the repository. Simply navigate into it and you will be inside the repository. Run `git status` to make sure you are in a valid git repo.
```
Bucky@Badgerloop~$: git status
On branch master
Your branch is up-to-date with 'origin/master'.
```
## Step 2: Create a seperate Branch
Before we make any commits, we have to talk about branching. Say you want to make a new feature but are worried about making changes to the main project. This is where **git branches** come into play.

One important branch is the **master** branch. This is reserved for our production ready code. Generally, you finish a feature before making it a part of master. On all Badgerloop Repos this is a locked branch requiring a review in order to make changes to master.

Branches allow you to move back and forth between different "states" of a project. All work done in Badgerloop will take place in a seperate branch before being a part of master. This way each member can work on a sub-project without interfering with other's work.

Let's create a branch by using the `git checkout` command with the `-b` flag. Let's create a branch called `{yourname}_tutorial` and confirm with the `git branch` command.

```
Bucky@Badgerloop~$: git checkout -b Bucky_tutorial
Bucky@Badgerloop~$: git branch
* Bucky_tutorial
  master
```
## Step 3: Add a new file to the Repo
Let's add a new file to the project. For this we are going to use the `touch` command. `Touch` will create an empty file. Create a text file titled by your first name.
```
Bucky@Badgerloop~$: touch Bucky.txt
Bucky@Badgerloop~$: ls
README.md Bucky.txt
```

After creating the new file, you can use the `git status` command to see which files git knows about.

```
Bucky@Badgerloop~$: git status
On branch Bucky_tutorial
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        Bucky.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
Basically, this means "Hey, we noticed you make a new file called Bucky.txt but unless you use the `git add` command, we aren't going to do anything about it.

## Step 3.5: The Staging Enviroment
Git works on a concept called the staging enviroment, this is one of the most confusing parts of git. Let's go through some terminology.

### Commit
A commit is a record of what files you have changed since last time you made a commit. Essentially you make changes to the repo (either by adding, deleting, or modifying files) and you "commit" to your changes by telling git to put those files into a commit.

This is where the version control comes in. You can backtrack to any previous commit at any point.

### Staging Enviorment
So, how do you tell git which files to put into a commit? This is where the staging enviroment comes in. As seen in Step 2, when you make changes to your repo, git notices that a file has changed but won't do anything with it. **Git will not automatically add your files to a commit**

## Step 4: Add a File to the Staging Enviroment
Add a file to the staging enviroment by using the `git add` command
```
Bucky@Badgerloop~$: git add Bucky.txt
Bucky@Badgerloop~$: git status
On branch Bucky_tutorial
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   Bucky.txt
```
## Step 5: Commit Your Changes
It's time to create your first commit!

Run the `git commit -m "{Your commit message}` command.

The `-m` flag means the next string will be a commit message. It is important to create meaningful commit messages so everyone knows what changes were made. It could be a new feature, fixing a bug, or even just fixing a typo. Please, please, please dont type "asdfasdfasdf" or "whatever". 

```
Bucky@Badgerloop~$: git commit -m "Added Bucky.txt to mark my contribution"
[Bucky_tutorial (root-commit) b345d9a] Added Bucky.txt to mark my contribution
 1 file changed, 1 insertion(+)
 create mode 100644 Bucky.txt
 ```

 ## Step 5.5: A Better Way

 When working with several files, it gets tedious to list every single file for one commit. An easier way to commit several files is to run the `git commit` command with the `-am` flag. As we learned eariler `-m` means you're adding a message to your commit. The `-a` flag means you want to commit all changed files. 
 ```
 Bucky@Badgerloop~$: git commit -am "Added Bucky.txt to mark my contribution"
 [Bucky_tutorial (root-commit) b345d9a] Added Bucky.txt to mark my contribution
 1 file changed, 1 insertion(+)
 create mode 100644 Bucky.txt
 ```

## Step 6: Push a branch to GitHub

Now that we are done with our change, we are ready to **push** it to GitHub. This allows other people to see the changes you've made, and eventually be put into master.

To push changes on a new GitHub Branch we'll use the `git push origin {your branch name}` command. Origin is just an alias for the repository's url.

```
Bucky@Badgerloop~$: git push origin Bucky_tutorial
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 313 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/Badgerloop-Software/github-tutorial.git
 * [new branch]      Bucky_tutorial -> Bucky_tutorial
```

At this point it may ask you to log in with your username and password.

Finally, if you refresh the GitHub page, you'll see a note of recently pushed branches, yours may be there, or click the "branches" link to see your branch listed there.

## Step 7: Creating a Pull Request

A pull request (or PR) is a way to alert the team leads that you want to make some changes to the codebase. It allows them, as well as other Badgerloop members to review the code and make sure it looks good before putting your changes on the master branch.

To start a pull request. Click the "New Pull Request" button on next to your branch.

![pull request image](https://i.imgur.com/ODualXT.png)

Be sure to give your PR a meaningful title and description. On the Software team we have a checklist of self-checks to go through before you post a PR. You may see a big green button at the bottom that says "Merge Pull Request" Clicking this means you'll merge your changes into the master branch. 

***Note If you are doing this tutorial as part of a Software Meeting, you will be required to get a review as if it was a real PR***

Note that this button won't always be green. In some cases it'll be grey, which means you're faced with the dreadded *merge conflicts*. This is when there is a change in one file the conflicts with a change somewhere else (either in that file or elsewhere) and git can't figure out which version to use. You'll have to manually go in an tell git which version to use.

Once the button is green, go ahead and click it. This will merge your changes into the master branch. When you're done, click delete branch as well. This will help with clutter.

## Step 8: Update the Files on Your Computer

Right now the repo on GitHub looks a little different than what you have on your computer. For example, the merge commit you just made doesn't exist on your local machine. We need to get the most recent changes with a `git pull` command.

```
Bucky@Badgerloop~$: git checkout master
Switched to branch 'master'
Bucky@Badgerloop~$: git pull
remote: Counting objects: 1, done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From https://github.com/badgerloop-software/github-tutorial
 * branch            master     -> FETCH_HEAD
   b345d9a..5381b7c  master     -> origin/master
Merge made by the 'recursive' strategy.
 Bucky.txt | 1 +
 1 file changed, 1 insertion(+)
 ```

## Step 9: Give yourself a Pat on the Back

Yahoo, you've sucessfully contributed to a repository! Congratulations, this is the foundation of writing code for the Badgerloop teams and will be used nearly every time you work with Badgerloop Software.

Good luck in your future quest to git gud :)
