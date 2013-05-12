## Git Walkthrough

### Getting started

Here are the steps I'm taking to write a template and get it onto the main shared repo - "jellybean."

You should already have created a fork off of jellybean in your github account (click the fork button) - this is "origin". If you haven't already, get a local copy of your github repo on your computer:
    $ git clone https://github.com/esoergel/coderaising.git
    $ cd coderaising/

Add Ted's repo as a remote repository called jellybean
    $ git remote add jellybean git://github.com/tedtieken/coderaising.git

You can also add the coderaising/coderaising repo (which we refer to as coderaising)

Check what remote repositories you have
    $ git remote
    jellybean
    origin
    coderaising

See information about jellybean
    $ git remote show jellybean

Look at all remote branches
    $ git branch -r

Check what branches you have.
    $ git branch
    * develop
      feature/wiki  # you probably won't have this one
      master

Fetch all the branches from jellybean
    $ git fetch jellybean

Checkout a branch (this won't save it, that's coming up).  Note that "jellybean/develop" is exactly the same as the way you saw that branch listed when you ran "git branch -r".
    $ git checkout jellybean/develop
    # here you'll get some useful information
Type git branch and it'll show that you're on (no branch).  This is how you can look at someone else's work, poke around, and save it if you want (but you don't have to). To save it as a local branch called develop, run
    $ git checkout -b develop

Better yet, perform that whole last block in one step(but without the opportunity to poke around before saving)
    $ git checkout -b develop jellybean/develop

Anyways, that pretty much covers how to get started.  Let me know if I'm missing anything or made any mistakes/bad pratices (I'm still learning this).

----------------------------------------------------------------------
### Branching

Now, on to making changes and what not.  You should be comfortable with git add and git commit already.  The method of branching is a style and consistency thing, it'll work if you don't follow our branching model strictly, but we've should stick to best practices.  For us, that means that work is all done on a feature branch.  I'm keeping "develop" in line with the develop branch on jellybean, even though there are other ways to do it.

First I check what branch I'm on and switch over to develop.
    $ git branch
      develop
      feature/wiki
    * master
    $ git checkout develop

Pull any changes that have been made on the jellybean develop branch since I last updated.
    $ git pull jellybean develop
    # blah blah, up-to-date.  Good.

Okay, make a new fork called feature/dummy_templates (for mine)
    $ git branch feature/dummy_templates

Now there is a branch that's an exact copy of develop. If you run git branch, you'll see you're still on develop, so switch to the new branch
    $ git checkout feature/dummy_templates

NOW you can actually make changes and commit them.  In the future I'm not sure if we'll actually branch this much, but branches and merges are cheap and easy, so it doesn't hurt.

----------------------------------------------------------------------
### short Django interlude

I started a new django app called "core" within the project to house some views.
    $ cd apps/
    $ django-admin.py startapp core

I then added/modified the following files.  I recommend opening all of them to trace the flow of execution and mirror changes I made to build your templates.
    * urls.py
    * apps/core/views.py
    * apps/theme/static/css/dummy.css
    * apps/theme/templates/dummy.html

----------------------------------------------------------------------

### Pushing changes

Check what changes you made
    $ git status

Add all of them (or add them individually) and commit.
    $ git add .
    $ git commit -m "added a dummy template and tied it in to the urlconf and views"

Switch over to your develop branch and pull from jellybean to make sure it's up-to-date.
    $ git checkout develop
    $ git pull jellybean develop

Switch back to your feature branch and merge in develop
    $ git checkout feature/dummy_templates
    $ git merge develop
    # hope there were no merge conflicts

Now your branch should include all public changes to develop, plus your own, and yours is the most up-to-date.  Make it public!

Push all your branches to your github repo (origin)
    $ git push --all
    # this is the same as:
    $ git push origin --all

Now anyone can pull your changes directly from there in the same way they pull from jellybean (but they'd have to add your repo as a remote).  Since jellybean is our main remote repo, issue a pull request to update jellybean/develop with your branch.

### Github pull request

1. Go to your github repo: https://github.com/esoergel/coderaising/
1. Click Pull Request at the top
1. To send "feature/dummy_templates" from "esoergel/coderaising" to "develop" on "tedtieken/coderaising," your boxes should look like this:
    base repo: tedtieken/coderaising        head repo: esoergel/coderaising
    base branch: develop                    head branch: feature/dummy_templates
1. Write a message exactuallyplaining what changes you're trying to get pulled in.

Then sit back and wait for your request to get approved.  Congratulations, you've just contributed to an open source project!!



------------------------------
End note:
I'm new to this, so I wrote this walkthrough as much to solidify my understanding as to explain it to others.  I might've missed some best practices, or there could be better was/orderings to do things.  If you have any comments, please let me know via the issues tracker or wiki