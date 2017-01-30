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

##Remotes

##Pushing your changes

##Pulling changes from a remote repository

##Fetching from a remote repository

##Branching

##Tagging

##Stashing current changes

##Merging changes from a branch

##Hooks

