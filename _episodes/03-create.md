---
title: Creating a Repository
teaching: 10
exercises: 0
questions:
- "Where does Git store information?"
objectives:
- "Create a local Git repository."
keypoints:
- "`git init` initializes a repository."
---

Once Git is configured,
we can start using it.
Let's create a directory for our work and then move into that directory:

~~~
$ mkdir breakfast
$ cd breakfast
~~~
{: .bash}

Then we tell Git to make `breakfast` a [repository]({{ page.root }}/reference/#repository)—a place where
Git can store versions of our files:

~~~
$ git init
~~~
{: .bash}

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

~~~
$ ls
~~~
{: .bash}

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `breakfast` called `.git`:

~~~
$ ls -a
~~~
{: .bash}

~~~
.	..	.git
~~~
{: .output}

Git stores information about the project in this special sub-directory.
If we ever delete it,
we will lose the project's history.

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

~~~
$ git status
~~~
{: .bash}

~~~
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
~~~
{: .output}

> ## Places to Create Git Repositories
>
> We start a new project, `family_recipes`, related to our `breakfast` project.
> We enter the following sequence of commands to
> create one Git repository inside another:
>
> ~~~
> $ cd                      # return to home directory
> $ mkdir breakfast              # make a new directory breakfast
> $ cd breakfast                 # go into breakfast
> $ git init                # make the breakfast directory a Git repository
> $ mkdir family_recipes    # make a sub-directory breakfast/family_recipes
> $ cd family_recipes       # go into breakfast/family_recipes
> $ git init                # make the family_recipes sub-directory a Git repository
> ~~~
> {: .bash}
>
> Why is it a bad idea to do this? (Notice here that the `breakfast` project is now also tracking the entire `family_recipes` repository.)
> How can we undo our last `git init`?
>
> > ## Solution
> >
> > Git repositories can interfere with each other if they are "nested" in the
> > directory of another: the outer repository will try to version-control 
> > the inner repository. Therefore, it's best to create each new Git
> > repository in a separate directory. To be sure that there is no conflicting
> > repository in the directory, check the output of `git status`. If it looks
> > like the following, you are good to go to create a new repository as shown 
> > above:
> >
> > ~~~
> > $ git status
> > ~~~
> > {: .bash}
> > ~~~
> > fatal: Not a git repository (or any of the parent directories): .git
> > ~~~
> > {: .output}
> >
> > Note that we can track files in directories within a Git:
> >
> > ~~~
> > $ touch dad mom aunt_phoebe maria               # create recipe files
> > $ cd ..                                         # return to breakfast directory
> > $ ls family_recipes                             # list contents of the family_recipes directory
> > $ git add family_recipes/*                      # add all contents of breakfast/family_recipes
> > $ git status                                    # show family_recipes files in staging area
> > $ git commit -m "add recipes from relatives"    # commit breakfast/family_recipes to breakfast Git repository
> > ~~~
> > {: .bash}
> >
> > Similarly, we can ignore (as discussed later) entire directories, such as the `family_recipes` directory:
> >
> > ~~~
> > $ nano .gitignore # open the .gitignore file in the texteditor to add the family_recipes directory
> > $ cat .gitignore # if you run cat afterwards, it should look like this:
> > ~~~
> > {: .bash}
> >
> > ~~~
> > family_recipes
> > ~~~
> > {: .output}
> >
> > To recover from this little mistake, we can just remove the `.git`
> > folder in the family_recipes subdirectory. To do so we can run the following command from inside the 'family_recipes' directory:
> >
> > ~~~
> > $ rm -rf family_recipes/.git
> > ~~~
> > {: .bash}
> >
> > But be careful! Running this command in the wrong directory, will remove
> > the entire git-history of a project you might wanted to keep. Therefore, always check your current directory using the
> > command `pwd`.
> {: .solution}
{: .challenge}
