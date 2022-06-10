---
title: Push to Git from the CLI
layout: post
categories: linux
tags: [git]
---

Now that I'm writing posts using `Nano`, I needed to figure how to push changes to `GitHub 
Pages` from the command line. 

<!--more-->

### Install gh
We need to install `gh`. Full instructions can be found 
[here](https://github.com/cli/cli/blob/trunk/docs/install_linux.md){:target="_blank"}.

### Login to GitHub
Next, we need to login to GitHub. Begin by changing directory into the directory that holds 
the local version of your project. Then enter the command

```
gh auth login
```

Follow the instructions. 

### Status
Run the command

```
git status
```

This will list the files yet to be committed. 

### Unstaged Files
Add any newly created files to the unstaged list using the command

```
git add .
```

### Commit
To commit the changes, run the command

```
git commit -a
```

A list of files available to commit will pop up in your text editor, each preceded by a 
`#`. Remove the hash for each file you want to commit, and then save and exit from the list. 

### Push
To push the changes to the main branch of the remote repository, run the following;

```
git push origin main
```

Give it a few minutes and you should see the changes appear on your web site. 
