# WuLug Workshop

## git: free, open-source, distributed version control system
**git** is a simple, easy to use version control system
This exercise is available at https://github.com/soleluke/exercises

Most information for this exercise was pulled from the official Git documentation at https://git-scm.com/docs

### Initializing a repository
Make a test directory in your home directory
```
	mkdir ~/git-test
	cd ~/git-test
```
#### Standard Repository
```
	mkdir normal
	cd normal
	git init
```
#### Bare Repository
```
	cd ~/git-test
	mkdir bare
	cd bare
	git init --bare
```
### Cloning a repository
```
	cd ~/git-test
	git clone https://github.com/soleluke/exercises.git
```
This should clone the 'exercises' repository into a directory called 'exercises'. This directory can be renamed after cloning without affecting the repository
### Adding/Removing Files
```
	cp exercises/tmux.md normal/
	cd normal
	git status
```
```
	git add tmux.md
```
### Ignoring a file at the repository level
Lets say you have a configuration file that contains information you dont want included in the repo
```
	mkdir .config
	cd .config
	echo "secrets" > ex.conf
	cd ..
	echo ".config" > .gitignore
	git status
```
Note that the only change that git is noticing is the addition of .gitignore
```
	git add .gitignore
```
### Commiting your changes
At this point, you have made changes in the repository. We need to save (or commit) these changes.
Since all of our files are added to the repository, committing is as simple as running
```
	git commit
```

This will pull up the default git text editor. This can be configured using `git config --global core.editor "nano"`
To bypass the text editor for commit messages, use
```
	git commit -m "<your-commit-message-here>"
```
If you have not set certain config items for git, you may receive the following message when you make this commit:
```
Your name and email address were configured automatically based on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly:

    git config --global user.name "Your Name"
	git config --global user.email you@example.com

After doing this, you may fix the identity used for this commit with:

	git commit --amend --reset-author

```
Follow those instructions to set your configuration and amend your commit

### Remotes
Having a local git repository is nice, but the collaborative power of git comes from using shared remote repositories (i.e. GitHub, BitBucket).
Lets go back to the exercises folder
```
	cd ~/git-test/exercises
```
Since we started by cloning a repo, we already have a remote set up for us
```
	git remote show origin
```
The origin remote is automatically created for any repository created with `git clone` for convenience.
Additional remotes can be created using
```
	git remote add <remote-name> <remote-url>
```
### Pushing your changes
Try running `git push`
This should cause an error or prompt you to login to github. One of the key concepts about git is that everyone must have the proper permissions to perform an action on a remote.
Since you do not have write access to the repository, you cannot push to the remote.

### Pulling changes from a remote repository
To retrieve the latest version of the branch you are working on, use `git pull`. Since we cloned the 'exercises' repo at the beginning of the exercise, there probably wont be any changes, so git will tell you that we are already up-to-date
### Fetching from a remote repository
Git maintains the repository information separately from what is known as the 'working copy' of the code. When you use `git pull`, your working copy is updated to the latest that you pulled. But what if you dont want to change your working copy, but still have the most up to date version?
This is where fetching come in. running `git fetch <remote>` grabs the repository information and updates your local copy of it, without touching your working copy. You can apply these changes by merging them (merging will be covered later in the excercise).
### Branching
Thus far, we have been making all changes on the master branch of the repository. This is not best practice in development environments, especially in collaborative ones
Let's make a new branch to work on and switch to it
```
	cd  ~/git-test/normal
	git branch development
	git checkout development
```

This creates the branch 'development' and switches to (or checks out) it.

Make some changes on this branch, then commit them.
```
	echo 'testing branching' >> branching
	git add branching
	git commit -m "testing branching"
```
Switch back to the master branch using `git checkout master`
Notice how the file 'branching' does not exist?
Check out development and it returns
To push your additional branch, simply specify the branch when pushing.
The -u flag in the command sets the upstream branch. This connects your local branch to the remote branch when you pull, thus removing the need to specify which branch you are pulling. It is best advisable to use the -u flag the first time you push a local branch to a remote.
```
	git push -u <remote> <branch-name>
```
### Tagging
Git implements a tagging system that lets you easily identify different commits.
Lets say you just released version 1.0 of this repository and you want to easily check what commit that is
```
	cd ~/git-test/normal
	git checkout master
	git tag -a v1.0 -m "Version 1.0"
```
We just created what is known as an annotated tag (-a flag indicates this). This contains a message with the tag
We can now easily view the contents of the commit that we have tagged
```
	git show v1.0
```
This displays both the Tagger, the message, the date of the tag and the contents of the commit.

Lightweight tags do not contain any extra information
```
	git tag v1.0-lw
	git show v1.0-lw
```
Note the differences in what is displayed between the two tags
### Stashing current changes
Sometimes, you need to make changes on a clean working directory, but have changes that are not ready for a commit, but you dont want to lose them

This is where stashes come in.
```
	git checkout development
	echo "stashing this change" >> stashing
	git add stashing
	git status
```
Git has registered our changes. Now let's stash them
```
	git stash save 
```
Note how the 'stashing' file has now disappeared and we are back to the way it was. At this point, we could pull more changes in, make commits, etc like normal
Let's reapply our stash
```
	git stash list
```
This lists all stashes that can be applied
```
	git stash apply stash@\{0\}
```
Note that the file 'stashing' has returned
Finish off by committing the changes
### Merging changes from a branch
At this point, development has some changes that we want to apply to the master branch.
This is known as merging. There are many different scenarios for merging. This exercise covers a basic one
First checkout the master branch using `git checkout master`
Next, we do our merge from development. You can merge using any tag, branch, or commit.
```
	git merge development
```
In this scenario, since the only difference was that there were commits between the two branches, a "fast-forwad" is performed
In other cases, git will alert you hat there was a merge conflict, insert information into the conflicting files and request that you fix the conflict and then commit those change
### Hooks
Remember that bare repository that we created back up top? We are going to use that.
Switch to the bare repository directory
```
	cd ~/git-test/bare/hooks/
	ls
```
Note that there is a directory called 'hooks'
Hooks in the context of git are scripts that will be run in given scenarios
Running the `git init --bare` creates some sample hooks in the hooks directory
Lets view one of these
```
	cat post-update.sample
```
We are going to make a post-receive hook for this bare repository.
```
	echo -e '#!/bin/bash\necho $(date) >> ~/test.log' >> post-receive
	chmod +x post-receive
```
This will put the current date into the test.log file every time the repository receives something
Lets add our bare repo as a remote and push to it
```
	cd ~/git-test/normal
	git remote add test-bare ~/git-test/bare
	git push test-bare master
```
Run `cat ~/test.log` and check if our script ran

Since hooks can be any sort of executable, git can automatically do a lot for you.
