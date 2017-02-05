#WuLug Workshop: git; free, open-source, distributed version control system
**git** is a simple, easy to use version control system
This exercise is available at https;//github.com/soleluke/exercises

Most information for this exercise was pulled from the official Git documentation at https://git-scm.com/docs

##Initializing a repository
Make a test directory in your home directory
```
	mkdir ~/git-test
	cd ~/git-test
```
###Standard Repository
```
	mkdir normal
	cd normal
	git init
```
###Bare Repository
```
	cd ~/git-test
	mkdir bare
	cd bare
	git init --bare
```
##Cloning a repository
```
	cd ~/git-test
	git clone https;//github.com/soleluke/exercises.git
```
This should clone the 'exercises' repository into a directory called 'exercises'. This directory can be renamed after cloning without affecting the repository
##Adding/Removing Files
```
	cp exercises/tmux.md normal/
	cd normal
	git status
```

```
	git add tmux.md
```


##Ignoring a file at the repository level
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
##Commiting your changes
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
##Remotes
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
	git remote add <remote-name>
```
##Pushing your changes
Try running `git push`
This should cause an error. One of the key concepts about git is that everyone must have the proper permissions to perform an action on a remote.
Since you do not have write access to the repository, you cannot push to the remote.

##Pulling changes from a remote repository
To retrieve the latest version of the branch you are working on, use `git pull`. Since we cloned the 'exercises' repo at the beginning of the exercise, there probably wont be any changes, so git will tell you that we are already up-to-date
##Fetching from a remote repository

##Branching

##Tagging

##Stashing current changes

##Merging changes from a branch

##Hooks

