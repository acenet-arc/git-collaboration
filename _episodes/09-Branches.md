---
title: "Branches"
teaching: 0
exercises: 0
questions:
- "Learn how to work with branches."
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
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

## Creating and switching branches
> ## Git Sandbox
>
> We will practice a bit in an online "Git Sandbox" at:
> [https://pcottle.github.io/learnGitBranching/?NODEMO][learnGitSandbox]
>
> The *Git Sandbox* lets us use simplified commands such as `git add`, `git commit`, `git status`, 
> `git checkout`, `git branch`, `git merge`. In this simplified environment we can skip the steps of
> creating and modifying files. Even the use of `git add` is optional and we will skip it for brevity.
>
> {: .source}
{: .callout}

1. We start with a git repo that has two commits (*c0* and *c1*) and a single branch `main` at *c1*, 
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

2. Next we create a new branch with `git branch feature1` and make a commit: `git commit` (*c2*):

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

3. We switch to the branch `feature1` with `git checkout feature1` and make a commit (*c3*) with 
   `git commit`:
   
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
   
4. Let's make two more commits (*c4* and *c5*) to the `feature1` branch:
   
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

5. We start working on a second feature. First we switch back to our main branch (`git checkout main`),
   before creating a new one. This time we combine creating a new branch and switching to it in a 
   single command: `git checkout -b feature2`, followed by a commit (*c6*):

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

6. Someone found a bug in our `main` branch, that was likely introduced with *c2*, so `feature1` is
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

## Merging branches

The `bugfix3` has quickly been tested and reviewed (it was a quite simple fix), so we now want to 
merge it into the `main` branch. 

1. First we need to change to the `main` branch `git checkout main`:

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

2. We use `git merge bugfix3` to merge the branch `bugfix3` into the current branch `main`:

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


3. Our colleague reports back to us on `feature1` and made a small change (*c9*), which we now want
   to pull into our local `feature1` branch.  As we don't want to pull it into the `main` branch just
   yet, we switch to the `feature1` branch with `git checkout feature1` and then use 
   `git pull origin feature1` to pull the commit to our current branch.
   
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

4. After one more round of testing, we decide that `feature1` is ready to be merged into `main`.
   We `git checkout main` and then use `git merge feature1`.  This is not a fast-forward merge as 
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

## Cleaning up

1. We can now delete the branch `bugfix3`, because we no longer need it. We do this with the command
   `git branch -d bugfix3`:

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

2. What will happen if we want to delete branch `feature2`?

   ~~~
   $ git branch -d feature2
   ~~~
   {: .bash}
   ~~~
   $ git branch -d feature2
   error: The branch 'feature2' is not fully merged.
   If you are sure you want to delete it, run 'git branch -D feature2'.
   ~~~
   {: .output}

   > ## Careful when deleting un-merged branches.
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
   {: .callout}

   <div class="mermaid">
   flowchart RL
       c0((c0))
       c1((c1)) ==> c0
       c2((c2)) ==> c1
       c3((c3)) ==> c1
       c4((c4)) ==> c3
       c5((c5)) ==> c4
       c6((c6)) --> c2
       c7((c7)) ==> c2
       c8((c8)) ==> c7
       c9((c9)) ==> c5
       c10((c10)) ==> c8
       c10((c10)) ==> c9
   
       l1([main]) --> c10
       HEAD([HEAD]) --> l1
   
       classDef label fill:#ff1,stroke:#333,stroke-width:2px;
       classDef head fill:#f81,stroke:#333,stroke-width:2px;
       classDef commit fill:#D0D0FF,stroke:#9370DB,stroke-width:2px;
       classDef lostcommit fill:#D0D0FF,stroke:#9370DB,stroke-width:2px,opacity:0.4;
       linkStyle 5 opacity:0.3;
       class l1,l2,l3,l4 label
       class HEAD head
       class c10 commit
       class c6 lostcommit
   </div>

   Commit c6 is not lost right away but still remains in the depth of the git repo until the garbage
   collection will remove it. 
   The only way we can get it back is if we still have a record of the commit ID.


## Recap

> ## Git commands for managing branches
>
> * `git branch branchname` creates a new branch `branchname` from the currently checked-out commit.
> * `git checkout branchname` switches the workspace to the branch `branchname`.
> * `git checkout -b bname` combines the commands `git branch bname` and `git checkout bname`
>   and creates the new branch `bname` and switches to it with the same command.
> * `git merge bname` merges the branch `bname` into the currently active branch.
>   It's always the currently active (checked-out) branch that is being changed.
{: .checklist}

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
