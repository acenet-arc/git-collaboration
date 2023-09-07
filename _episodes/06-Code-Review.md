---
title: "Code Review"
teaching: 15
exercises: 5
questions:
- "Why should I do Code Review and how can I do it?"
objectives:
- "Learn how to review someone's pull request."
keypoints:
- "Code review increases code quality."
- "The reviewer checks whether the contribution conforms to the set standards."
- "When has >>I promise I'll write the documentation/tests later!<< ever worked?"
- "A second pair of eyes might find a more elegant solution."
- "The reviewer might learn something new when reading someone else's code."
---

Code Review is a practice in software development, where one or more other
human "reviewers" read the source-code contributions of a contributor before
they are merged into the project.

This is done for many reasons, e.g the ones listed by [Wikipedia][wp-code-review]:

> ## Goals of Code Review
> * **Better code quality**  - improve internal code quality and maintainability
>   (readability, uniformity, understandability, ...)
> * **Finding defects**  - improve quality regarding external aspects, especially
>   correctness, but also find performance problems, security vulnerabilities,
>   injected malware, ...
> * **Learning/Knowledge transfer**   - help in transferring knowledge about
>   the codebase, solution approaches, expectations regarding quality, etc;
>   both to the reviewers as well as to the author
> * **Increase sense of mutual responsibility**  -  increase a sense of collective
>   code ownership and solidarity
> * **Finding better solutions**  - generate ideas for new and better solutions
>   and ideas that transcend the specific code at hand.
> * **Complying to QA guidelines**  - Code reviews are mandatory in some
>   contexts, e.g., air traffic software
{: .callout}

It is indeed considered to be a good practice, as long as happens in a respectful
manner and with constructive criticism between the reviewer and the contributor.

Some projects even enforce that every pull request has to be reviewed by at
least a certain number of other developers (this feature is often part of the
non-free plans of Git-Collaboration sites).

Once a pull request has been opened, you can go to the pull request (in the
destination repository, click on the "Pull requests" tab, select it from the list)
and then go to the "Files changed" tab.
There the reviewer can read all proposed changes that are part of the pull request -
(added lines are highlighted green, removed ones red and changed lines show the
old version in red and new one in green) - and then click on the [+] icon next
to a line and leave a related comment with suggestions and continue with other
lines and files.

![Screen Shot of Code review]( {{ site.baseurl }}{% link fig/code-review.png %} )

Here it is important for the reviewer to leave constructive feedback and if possible
an explanation on why they think something should be done in a different way.
A reviewer can also ask for clarification on certain parts of the code, which might
be an indication that the implementation is too complex or is lacking documentation.

Finally reviewers, contributors as well as other users can leave comments on the
"Conversation"-tab to discuss the change.

The contributor will get notifications about new comments to the pull request
and can read the comments and reply to them. Further the contributor
can implement the agreed upon changes and commit and push them to their repository.

> **All commits that are pushed to the branch will be appended to the pull request.**
{: .callout}

> ## Review a Pull Request
>
> In the last lesson all attendees have opened a pull request towards the
> instructor's repository. Identify the pull request opened by your neighbor
> and review it by adding a few comments to the "changed files".
>
{: .challenge}



{% include links.md %}
