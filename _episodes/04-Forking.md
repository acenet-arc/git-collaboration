---
title: "Forking a Repository"
teaching: 5
exercises: 3
questions:
- "How can I make an online copy of a repository on which I can work?"
objectives:
- "Create an online copy of a repository under your own account."
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

Forking a repository on a Git hosting site creates a copy of the repository
under your own user-account, thereby keeping a link to the original repository.
This only works within the same platform, i.e. you need to have an account
on the same platform as the original repository.

When forking a repository, this basically runs `git clone ...` on the server.
The remote `origin` pointing to the original repository remains intact.

This allows us to contribute changes/commits back to the original repository
by a process called "Pull Request" or "Merge Request" (more on that later).

> ## Forks vs. Import
>
> Instead of forking a repository, you can also choose to import a repository.
> This also runs a `git clone ...` on the server, however removes the link
> to the original repository.  The two repositories are now separated and 
> independent from each other.
>
> Importing repositories also works across different platforms.
>
{: .callout}

When several people work on a software project, each developer typically
starts by forking the repository to their own user-account.  They then own
that copy and can work on implementing an enhancement or fixing a bug.

> ## Create a Fork
>
> 1. Go to your instructor's `testing_demo` repository on GitHub.
> 2. Click on the "Fork" button.
> 3. Wait a few moments until the repository has been copied
> 4. Explore your forked repository.
>
{: .challenge}

{% include links.md %}
