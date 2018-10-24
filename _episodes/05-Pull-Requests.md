---
title: "Pull-Requests and Code Review"
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

Pull Requests are a method of merging commits between repositories that have 
been forked. GitLab calls them "Merge Requests" but they are exactly the same
thing.  We will continue to call them "Pull Requests" in these lessons.
Often they are abbreviated as _PR_.

You can fork any repository that you have at least read-access to, start 
implementing an enhancement, fixing bugs or typos, improving documentation,
etc.  When you feel you are done with your improvement, you open a Pull-Request.

Like _Issues_ each Pull Request gets a unique ID, a title and an initial 
comment. Conversations are possible by posing additional comments.
In addition to that, all commits that have been made to the forked repository 
that are not already in the origin repository will be attached to the Pull-Request.

The owner of the original repository (or any developer who has been granted
sufficient rights by the owner) can **merge** the commits of the pull-request
into the original repository from the website.


> ## Submit a Pull Request
>
> 1. Go to your forked repository on the website.
> 2. Clone it to your Desktop using `git clone ...` in the Unix Shell:
>    ~~~
>    $ git clone https://github.com/<Your_GitHub_Username>/testing_demo.git
>    $ cd testing_demo
>    $ ls
>    ~~~
>    {: .language-bash}
>    ~~~
>    more_files  mean.py  README.md  Workflow.md
>    ~~~
>    {: ..output-bash}
> 3. Download the file `test_mean.py` and copy it into the cloned repo
>    (Into the same folder that contains `README.md` and `mean.py`).
> 4. Add the file `test_mean.py`, make a commit and push to GitHub:
>    ~~~
>    $ cp more_files/test_mean.py  ./
>    $ git add test_mean.py
>    $ git commit -m "adding unit tests"
>    $ git push origin master
>    ~~~
>    {: .language-bash}
> 5. Go back to the GitHub website and open a Pull-Request.
>
{: .challenge}
