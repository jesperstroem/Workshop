# Workshop
Welcome to the Git workshop!

## Preparation
### Install Git
First we need to install Git on your computer\
Download it here: https://git-scm.com/downloads \
Choose every default option when prompted\
\
When finished please open your Windows commandline and type "git -v"\
If it works correctly, it should look like the following:

![alt text](images/install.png)

### Create a Github user
Create a user at Github: https://github.com/ (If you do not already have one)

### Fork the workshop repository
The workshop tasks are found in a Github repository at: https://github.com/jesperstroem/Workshop\
To make it so you have your own personal copy of this repository, we need to "fork" it.\
While logged into your Github accound, go to https://github.com/jesperstroem/Workshop and press the down-arrow next to "fork" and then "Create a new fork".\
When the process is finished, you should see that you have a personal repository on Github, which is forked from mine.


## Workshop 1 - The basics
### Clone
The first task will be to clone your newly forked repository, such that you have it available on your local machine.\
In your shell, navigate to your desired folder and run the following commands (replace \<username> with your Github username):

    $ git clone https://github.com/<username>/Workshop.git
    $ cd Workshop
    $ ls -a

Now you should be able to see the files in the repository, which are copied from Github. Notice that there is also a .git folder, which tells you that you are dealing with a git repository.

### Add
Let's first add a new file to the working directory. Run the following command:

    $ echo "" > file.txt

This creates an empty .txt file in your working directory. This means it is not in your repository yet.\
Try to run `git status` and observe the output - Git has now noticed that you changed a file in the working directory.\
However it is not yet in the staging area. To do so, we use `git add`. Run the following:

    $ git add file.txt
    $ git status

What does `git status` tell you now? You have successfully added a file to the staging area!.\
Now let's say i want to change my file, because i made a mistake (such as in this case, where the file is empty and pretty useless).\
Run the following commands:

    $ echo "Useful content" > file.txt
    $ cat file.txt

Now what happens if you run `git status`? Observe that Git remembers what you have staged - however it also notices your new changes.\
To stage the new changes, simply run `git add file.txt` once more. Note that you can also run `git add .` to stage all changes in the working directory.

### Restore
Try to create a new file and stage it:

    $ echo "New content" > new_file.txt
    $ git add new_file.txt

The file is now ready for a commit. But what if we regretted adding this file to the staging area? We can fix that with `git restore`. Run the following:

    $ git restore --staged new_file.txt

Notice that the file is still in our working directory but that `git status` now shows the file as unstaged.
Run `git add new_file.txt` again to add it to the staging area once more.

### Commit
To commit your staged changes, run the following command:

    $ git commit -m "Added some useful content"

The -m option adds a commit message. This message should in broad terms say what changed for the commit.\
Now try to run `git status` and `git log`.\
`git status` should tell you that your local repository is now 1 commit ahead of the remote repository.\
`git log` should show you the commit history with your new commit.

### Pull
Our goal is to upload our newly created commit to the remote repository on Github. However, a good practice when doing so is to always run `git pull` before doing so.
In this case `git pull` will do nothing, since no one else has uploaded any commits to our repository. Run the following:

    $ git pull

Notice how Git will tell you that your local repository is already up to date with the remote repository.\
This means that we can safely "push" our new commit.

### Push
Run the following:

    $ git push

Notice the following pop-up from Github:\
![alt text](images/auth.png)

You are seeing this because you have not yet authenticated yourself with your Github repository - this means you can't push your changes just yet!\
Choose either option and follow the authentication flow. The push should happen automatically after this, and authentication should not be necessary in the future.

As a final task, try to run `git log`. Do you notice what is different in the logs?

### Extra
Try to go to the page of your Github repository and explore the information available.\
Can you see your changes? The new commit? What do you see if you pick a certain file and press "history" in the right-hand side of the web page?

Try to access new_file.txt on Github. Try to edit the file in the online editor and press "commit changes".\
Now in your computer's command window, try to run `git pull`. What happened?

### Summary
In workshop 1 you learned to use the following git commands:
- clone
- add
- status
- restore
- commit
- pull
- push

## Workshop 2 - Branches and merges
Using branches is a very powerful tool that will allow you to keep multiple separate versions of the repository in parallel.

# Creating branches

Try to run the following:

    $ git branch

This tells you which branches are currently available in your repository - there should only be a default "main" branch which every git repository will start with.\
Notice the * which tells you that you are currently on that branch - in other words, you have "checked out" the main branch.

To start a new branch run the following:

    $ git branch -b experiment

This will create a new branch called "experiment" and will automatically "check out" that branch.\
By running `git branch` you will notice the new branch and that the * has moved

Now you can simply run `git checkout <branch_name>` to switch between the branches. 

Notice that the branches at this point are completely identical, since the new branch "spawned" from the other branch, and we have not made any changes yet.

Check out the new experiment branch and run the following commands:

    $ echo "Now we are on another branch" > file.txt
    $ echo "The new branch has additional content" > new.txt

This edits the existing "file.txt" and adds another file called "new.txt".

Run `git add .` and `git commit -m "Commit on new branch"`.\
Then run `git pull` - why does this fail?

The answer is pretty simple - your new branch is not linked to any remote branch, so git does not know where to pull from!

We can easily fix this by running:

    $ git push --set-upstream origin experiment

This tells git to push to a new remote branch called origin/experiment and links the local and remote branch together.\
Try to run `git branch -a` to see all branches in the repository including the remote ones.\
Run `git status` to verify that the local branch is up to date with the remote branch.\
Try to switch back and forth between the main and experiment branch with `git checkout <branch>` and observe the files in the working directory changing.\
As a last effort, have a look at Github and explore your branch history. "Insights" -> "Network" will give you a visualization of your branch and commit history.

Congratulations - you now know how to keep multiple versions of your code!

### Merging

### Fixing merge conflicts

### Summary
In workshop 2 you learned to use the following git commands:
- branch
- merge

## Workshop 3 - Using .gitignore

### Summary
In workshop 3 you learned to use the .gitignore file so that you can ignore files that should not be included in the version control.