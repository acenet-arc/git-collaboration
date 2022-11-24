---
title: "Branches"
teaching: 15
exercises: 15
questions:
- "What are git branches?"
- "Why, when and how are branches used?"
objectives:
- "Learn how to create branches."
- "Learn how to switch branches."
- "Learn how to merge branches."
- "Learn how to delete unused branches."
keypoints:
- "`git branch bname` creates a new branch `bname` from the currently checked-out commit."
- "`git checkout bname` switches the workspace to the branch `bname`."
- "`git checkout -b bname` combines the commands `git branch bname` and `git checkout bname` \
   and creates the new branch `bname` and switches to it with the same command."
- "`git merge bname` merges the branch `bname` into the currently active branch. \
   It's always the currently active (checked-out) branch that is being changed."
- "`git branch -d bname` deletes a branch that has been merged."
- "To delete un-merged branches, we have to force git to delete them by using `-D` instead of `-d`. \
   This is to prevent accidentally deleting those branches and loosing data."
---
{% include mermaid.html %}

## Why should we use branches?

Branches are used to manage different versions of a project. Typical uses of branches are:

* **main** development **branch** is maintained in working order
* **feature branches** are used to develop new features and/or other improvements
* **bug fix branches** are used to fix bugs
* code review and testing takes place before branches are merged into the main development branch
  to maintain quality of the code and avoid breaking the main development branch.

This has the advantage that even drastic or experimental changes can be tried in a separate branch 
without breaking the code in the main development branch.

## Git Sandbox

We will practice a bit in an online "Git Sandbox" at:
[https://learngitbranching.js.org/?NODEMO][learnGitSandbox]. This sandbox allows us to quickly explore a larger git repository history without spending time editing files and speeds up the commit process. It is a good way to gain experience quickly with processes that usually happen over weeks. However, the *Git Sandbox* isn't a 1:1 simulation of git and some commands operate a little differently than they do in git. Mostly though, we don't have to worry too much about that.

The *Git Sandbox* lets us use simplified commands such as:
* `git add`
* `git commit`
* `git status`
* `git checkout`
* `git branch`
* `git merge`
* `git clone`

In this simplified environment we can skip the steps of creating and modifying files. Even the use of `git add` is optional and we will skip it for brevity.

The *Git Sandbox* command `git clone` allows us to duplicate our simulated repository and simulate working with remote repositories.

*Git Sandbox* even has some commands that git doesn't. For example:
* `undo`
* `git fakeTeamwork`

The `undo` command will undo the last command you ran and the `git fakeTeamwork <branch> <num-commits>` allows us to fake work happening on our simulated "remote" repository.

> ## More *Git Sandbox* details
> For more details on using the *Git Sandbox* see its [github repository](https://github.com/pcottle/learnGitBranching). The *Git Sandbox* even has a built in tutorial which you can access [here](https://learngitbranching.js.org/) which covers both how to use the *Git Sandbox* and also using git.
{: .callout}

## Creating and switching branches

<ol markdown="1">
<li markdown="1"> We start with a git repo that has two commits (*c0* and *c1*) and a single branch `main` at *c1*, 
   which is active (checked-out) and therefore gets the label `HEAD` (as we have learned in the episode
   [Exploring History](https://swcarpentry.github.io/git-novice/05-history/index.html) in the lesson
   "Version Control with Git"):

   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       l1([main]) --> c1
       HEAD([HEAD]) --> l1
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       class l1 label
       class HEAD head
   </div>
</li>
<li markdown="1">
Next we create a new branch and make a commit (*c2*) with:
~~~
$ git branch feature1
$ git commit
~~~
{: .language-bash}

   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       l1([main]) --> c2
       l2([feature1]) --> c1
       HEAD([HEAD]) --> l1
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       class l1,l2 label
       class HEAD head
   </div>

   > ## What has just happened?
   > Q: Why did our commit *c2* end up in branch `main` and not in `feature1`?
   > > ## Solution
   > > A: Because `git branch` has only created a new branch but not switched the active branch.
   > {: .solution}
   {: .discussion}
</li>
<li markdown="1">
We switch to the branch `feature1` and make a commit (*c3*) with:
~~~
$ git checkout feature1
$ git commit
~~~
{: .language-bash}
   
   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       l1([main]) --> c2
       l2([feature1]) --> c3
       HEAD([HEAD]) --> l2
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       class l1,l2 label
       class HEAD head
   </div>
</li>
<li markdown="1"> Let's make two more commits (*c4* and *c5*) to the `feature1` branch:
~~~
$ git commit
$ git commit
~~~
{: .language-bash}
   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       c4((c4)) ==> c3
       c5((c5)) ==> c4
 
       l1([main]) --> c2
       l2([feature1]) --> c5
       HEAD([HEAD]) --> l2
 
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       class l1,l2 label
       class HEAD head
   </div>
   
   Even though the new feature is now complete, it needs code review and some thorough testing.
   We have pushed the feature1 branch to the remote repository with `git push origin feature1`. 

   While a colleague reviews the code, they check out this branch and start running some extensive
   tests systems.  Until that is done, we can start working on something else.

We can fake this in the git sandbox by running the below.
~~~
$ git clone
~~~
{: .language-bash}
This can be thought of a little bit as creating a remote copy of our repository, in which our colleague will work and push changes to.

</li>
<li markdown="1"> We start working on a second feature. First we switch back to our main branch before creating a new one.
~~~
$ git checkout main
~~~
{: .language-bash}

This time we combine creating a new branch and switching to it in a 
single command, followed by a commit (*c6*):
~~~
$ git checkout -b feature2
$ git commit
~~~
{: .language-bash}

   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       c4((c4)) ==> c3
       c5((c5)) ==> c4
       c6((c6)) ==> c2
 
       l1([main]) --> c2
       l2([feature1]) --> c5
       l3([feature2]) --> c6
       HEAD([HEAD]) --> l3
 
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       class l1,l2,l3 label
       class HEAD head
   </div>
</li>
<li markdown="1"> Someone found a bug in our `main` branch, that was likely introduced with *c2*, so `feature1` is
   not affected.  Our `feature2` is not ready yet, but we urgently need to get the bug fixed in `main`.
   We start by checking-out `main` and then create and switch to `bugfix3`.  
   
   > ## Challenge
   > **Q**: What commands do we need for that?
   > > ## Solution
   > > ~~~
   > > $ git checkout main
   > > $ git branch bugfix3
   > > $ git checkout bugfix3
   > > ~~~
   > > {: .language-console }
   > > or even shorter:
   > > ~~~
   > > $ git checkout main
   > > $ git checkout -b bugfix3
   > > ~~~
   > > {: .language-console }
   > {: .solution}
   {: .challenge}

   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       c4((c4)) ==> c3
       c5((c5)) ==> c4
       c6((c6)) ==> c2
 
       l1([main]) --> c2
       l2([feature1]) --> c5
       l3([feature2]) --> c6
       l4([bugfix3]) --> c2
       HEAD([HEAD]) --> l4
 
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       class l1,l2,l3,l4 label
       class HEAD head
   </div>

   We then make two commits (*c7* and *c8*) to the `bugfix3` branch:
~~~
$ git commit
$ git commit
~~~
{: .language-bash}

   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       c4((c4)) ==> c3
       c5((c5)) ==> c4
       c6((c6)) ==> c2
       c7((c7)) ==> c2
       c8((c8)) ==> c7
 
       l1([main]) --> c2
       l2([feature1]) --> c5
       l3([feature2]) --> c6
       l4([bugfix3]) --> c8
       HEAD([HEAD]) --> l4
 
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       class l1,l2,l3,l4 label
       class HEAD head
   </div>

The bug is fixed. Well done! Now we need to integrate that fix into the `main` branch, so that
others can use it.
</li>
</ol>

## Merging branches

The `bugfix3` has quickly been tested and reviewed (it was a quite simple fix), so we now want to 
merge it into the `main` branch. 
<ol markdown="1">
<li markdown="1">
First we need to change to the `main` branch 
~~~
$ git checkout main
~~~
{: .language-bash}

   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       c4((c4)) ==> c3
       c5((c5)) ==> c4
       c6((c6)) ==> c2
       c7((c7)) ==> c2
       c8((c8)) ==> c7

       l1([main]) --> c2
       l2([feature1]) --> c5
       l3([feature2]) --> c6
       l4([bugfix3]) --> c8
       HEAD([HEAD]) --> l1

       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       class l1,l2,l3,l4 label
       class HEAD head
   </div>

   > ## How does the merge work?
   > **Q**: What needs to happen, to get the commits *c7* and *c8* into the `main` branch?
   >
   > **A**: Essentially we need for *c8* to become the new state for the main branch.
   >   All that needs to be done is move the label for branch `main` two commits further down the tree.
   > <div class="mermaid">
   > flowchart RL
   >      c0((c0))
   >      c1((c1)) ==> c0
   >      c2((c2)) ==> c1
   >      c3((c3)) ==> c1
   >      c4((c4)) ==> c3
   >      c5((c5)) ==> c4
   >      c6((c6)) ==> c2
   >      c7((c7)) ==> c2
   >      c8((c8)) ==> c7
   >
   >      l1([main]) --> c2
   >      l2([feature1]) --> c5
   >      l3([feature2]) --> c6
   >      l4([bugfix3]) --> c8
   >      HEAD([HEAD]) --> l1
   >      l1 -.-> c8
   >
   >      classDef label fill:#ff1,stroke:#333,stroke-width:2px;
   >      classDef head fill:#f81,stroke:#333,stroke-width:2px;
   >      class l1,l2,l3,l4 label
   >      class HEAD head
   > </div>
   > 
   > This is also called a "Fast Forward" merge (FF-merge), because a branch-label is just moved 
   > along an existing chain of commits.
   {: .discussion}
</li>
<li markdown="1">
We use the `merge` command to merge the branch `bugfix3` into the current branch `main`.
~~~
$ git merge bugfix3
~~~
{: .language-bash}

   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       c4((c4)) ==> c3
       c5((c5)) ==> c4
       c6((c6)) ==> c2
       c7((c7)) ==> c2
       c8((c8)) ==> c7
   
       l1([main]) --> c8
       l2([feature1]) --> c5
       l3([feature2]) --> c6
       l4([bugfix3]) --> c8
       HEAD([HEAD]) --> l1
   
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       class l1,l2,l3,l4 label
       class HEAD head
   </div>

   Sure enough, all that has changed is which commit the label `main` points to.

</li>
<li markdown="1">
Our colleague reports back to us on `feature1` and made a small change (*c9*), which we now want
   to pull into our local `feature1` branch.

We can fake the work of our colleague in the git sandbox with
~~~
$ git fakeTeamwork feature1 1
~~~
{: .language-bash}
   
As we don't want to pull it into the `main` branch just yet, we switch to the `feature1` branch and pull in the changes to our current branch.
~~~
$ git checkout feature1
$ git pull origin feature1
~~~
{: .language-bash}
   
   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       c4((c4)) ==> c3
       c5((c5)) ==> c4
       c6((c6)) ==> c2
       c7((c7)) ==> c2
       c8((c8)) ==> c7
       c9((c9)) ==> c5
   
       l1([main]) --> c8
       l2([feature1]) --> c9
       l3([feature2]) --> c6
       l4([bugfix3]) --> c8
       HEAD([HEAD]) --> l2
   
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       class l1,l2,l3,l4 label
       class HEAD head
   </div>
</li>
<li markdown="1">
After one more round of testing, we decide that `feature1` is ready to be merged into `main`. We checkout the `main` branch and `merge` in the `feature` branch.
~~~
$ git checkout main
$ git merge feature1
~~~
{: .language-bash}
This is not a fast-forward merge as 
   branches `main` and `feature1` have diverged.  This merge will cause a merge commit *c10* to be
   created that combines the content of *c8* and *c9*.
   
   Git will do a fantastic job combining the content from both commits, however if the same line
   has been changed (or lines in close proximity) on both branches since their last common ancestor,
   git won't be able to resolve this on its own and will alert us of a conflict (which was covered 
   in Episode [Conflicts](https://swcarpentry.github.io/git-novice/09-conflict/index.html) of the
   lesson "Version Control with Git").  
   
   We are lucky and don't run into a conflict with this merge.
   
   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       c4((c4)) ==> c3
       c5((c5)) ==> c4
       c6((c6)) ==> c2
       c7((c7)) ==> c2
       c8((c8)) ==> c7
       c9((c9)) ==> c5
       c10((c10)) ==> c8
       c10((c10)) ==> c9
   
       l1([main]) --> c10
       l2([feature1]) --> c9
       l3([feature2]) --> c6
       l4([bugfix3]) --> c8
       HEAD([HEAD]) --> l1
   
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       classDef commit fill:#D0D0FF,stroke:#9370DB,stroke-width:2px;
       class l1,l2,l3,l4 label
       class HEAD head
       class c10 commit
   </div>
</li>
</ol>
## Cleaning up
<ol>
<li markdown="1">We can now delete the branch `bugfix3`, because we no longer need it. We do this with the command:
~~~
$ git branch -d bugfix3
~~~
{: .language-bash}

   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       c4((c4)) ==> c3
       c5((c5)) ==> c4
       c6((c6)) ==> c2
       c7((c7)) ==> c2
       c8((c8)) ==> c7
       c9((c9)) ==> c5
       c10((c10)) ==> c8
       c10((c10)) ==> c9
   
       l1([main]) --> c10
       l2([feature1]) --> c9
       l3([feature2]) --> c6
       HEAD([HEAD]) --> l1
   
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       classDef commit fill:#D0D0FF,stroke:#9370DB,stroke-width:2px;
       class l1,l2,l3,l4 label
       class HEAD head
       class c10 commit
   </div>

   Only the label for `bugfix3` was removed. As `main` points to the same commit that `bugfix3` used
   to point to, we don't have any "dangling commits" that we might loose access to.
   The branch `feature1` can be removed the same way.
</li>
<li markdown="1">
What will happen if we want to delete branch `feature2`?
This is actually a place where the *Git sandbox* diverges from git. Normally with git if you use the `-d` option to delete a branch, it won't delete a branch which isn't fully merged.
~~~
$ git branch -d feature2
~~~
{: .language-bash}
~~~
error: The branch 'feature2' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature2'.
~~~
{: .output}

However, in *Git Sandbox* it will happily do this.
</li>
</ol>
   > ## Be Careful When Deleting Un-merged Branches.
   >
   > Here Git warns us that we are about to delete a branch that has not been merged.
   > Without the "label" that is the branch name, we are about to loose access to those commits that
   > have not been merged.  Those commits could be irrevocably lost.
   >
   > The error message will tell us how we can delete the branch anyway.
   > As this feature was only an experiment and didn't quite turn out how we had hoped, we will 
   > in fact delete it:
   > 
   > ~~~
   > $ git branch -D feature2
   > ~~~
   > {: .language-bash}
   > 
   > <div class="mermaid">
   > flowchart RL
   >     c0((c0))
   >     c1((c1)) ==> c0
   >     c2((c2)) ==> c1
   >     c3((c3)) ==> c1
   >     c4((c4)) ==> c3
   >     c5((c5)) ==> c4
   >     c6((c6)) --> c2
   >     c7((c7)) ==> c2
   >     c8((c8)) ==> c7
   >     c9((c9)) ==> c5
   >     c10((c10)) ==> c8
   >     c10((c10)) ==> c9
   > 
   >     l1([main]) --> c10
   >     HEAD([HEAD]) --> l1
   > 
   >     classDef label fill:#ff1,stroke:#333,stroke-width:2px;
   >     classDef head fill:#f81,stroke:#333,stroke-width:2px;
   >     classDef commit fill:#D0D0FF,stroke:#9370DB,stroke-width:2px;
   >     classDef lostcommit fill:#D0D0FF,stroke:#9370DB,stroke-width:2px,opacity:0.4;
   >     linkStyle 5 opacity:0.3;
   >     class l1,l2,l3,l4 label
   >     class HEAD head
   >     class c10 commit
   >     class c6 lostcommit
   > </div>
> 
   > Commit c6 is not lost right away but still remains in the depth of the git repo until the garbage
   > collection will remove it. 
   > The only way we can get it back is if we still have a record of the commit ID.
   {: .callout}

## Homework

> ## Practice what you have learned.
> Working with branches can be a bit daunting at the start.  Please practice this for 
> yourself using the [guided tutorial from Learn Git Branching][learnGitBranching] 
> and/or experiment in their [Git Sandbox][learnGitSandbox] like we did in this lesson.
{: .challenge}

<!-----
> ## Callout Title
>
> <div class="mermaid">
> flowchart RL
>   c0((c0))
>   c1((c1)) ==> c0
>   l1([main]) -- > c1
>   HEAD([HEAD]) -- > l1
>   classDef label fill:#ff1,stroke:#333,stroke-width:2px;
>   classDef head fill:#f81,stroke:#333,stroke-width:2px;
>   class l1 label
>   class HEAD head
> </div>
> 
> 
> <div class="mermaid">
> flowchart RL
>   c0((c0)) 
>   c1((c1)) ==> c0
>   l1([main]) -- > c1
> 
>   classDef commit fill:#ECECFF,stroke:#9370DB,stroke-width:1px;
>   classDef label fill:#ff1,stroke:#333,stroke-width:2px;
>   class c0,c1 commit
>   class l1 label
> </div>
{: .solution}
----->

{% include links.md %}
