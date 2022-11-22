---
title: "Forking a Repository"
teaching: 5
exercises: 3
questions:
- "How can I make an online copy of a repository on which I can work?"
objectives:
- "Create an online copy of a repository under your own account."
keypoints:
- "By forking a repository you create a copy under your own account."
- "You can use this 'fork' to develop you own feature or fix a bug that's bugging you."
- "This can be the base for contributing these changes back to the original project."
- "Sometimes however it is used to initiate an independent spin-off that will diverge over time."
---
{% include mermaid.html %}

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
> 1. Go to **your instructor's** `testing_demo` repository on GitHub.
> 2. Click on the "Fork" button.
> 3. Wait a few moments until the repository has been copied
> 4. Explore your forked repository.
>
{: .challenge}

> ## Fork the correct repository!
>
> The idea here is that
> * the **instructor** forks the *original* (template) testing_demo repository and
> * the **workshop attendees** will fork the *instructor's fork* of the testing_demo repo.
>
> In the end, the fork-tree should look something like this for a workshop with
> five attendees:
>
> <div class="mermaid">
> flowchart RL
>   A( acenet-arc /<br />testing_demo ) ;
>   B[ instructor /<br /> testing_demo ] -- fork of --> A ;
>   subgraph Used in the workshop
>   C1[ attendee1 /<br /> testing_demo ] -- fork of --> B ;
>   C2[ attendee2 /<br /> testing_demo ] -- fork of --> B ;
>   C3[ attendee3 /<br /> testing_demo ] -- fork of --> B ;
>   C4[ attendee4 /<br /> testing_demo ] -- fork of --> B ;
>   C5[ attendee5 /<br /> testing_demo ] -- fork of --> B ;
>   end
> </div>
>
> The original repository will remain in its initial state and issues and
> pull-requests will only be created towards the *instructor's fork* of the repository.
{: .callout}

{% include links.md %}
