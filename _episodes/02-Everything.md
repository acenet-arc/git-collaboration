---
title: "Everything"
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

## Overview of Git hosting sites
* Many common features:
  * Usually free for Public repositories
  * Code Management
    * Git repositories
    * Browsing history
    * Branches
    * Web code editor
  * Forking
  * Pull/Merge requests
    * Code review
  * Issue Tracker
    * Milestones
  * Wiki (documentation / notes)
  * Rendering of Markdown files.
  * Group-accounts
    * Organizations (GH), Teams/Projects (BB), Groups (GL)
  * Snippets (GitHub: Gist)
  * Continuous Integration (CI, Pipelines)
    * limited number of CI-minutes per month for free

### Hosted Platforms
#### GitHub
* Biggest site
* Private repositories for a fee
* Free packages for Students, Teachers/Educators
* Hosting of static websites (GitHub pages)
* external Continuous Integration service: Travis-CI.com
* integrated with many 3rd party services

#### BitBucket
* Supports also Mercurial (`hg`) repositories
* Free private repositories (max 5 collaborators)
* Academic accounts (User and/or Team) with unlimited private repositories.

#### GitLab.com
* Free private repositories
* Hosting of static websites (GitLab pages)

### Self-Hosted
* Run a Git Hosting Platform on your own server.

#### GitLab Community Edition (CE)
* Open Source version of the software running on GitLab.com
* Almost all features of GitLab.com

#### Gitea
* Very lightweight but just the basic features

## Issues
Issues are being used for communication between *users* and *developers*.
These roles are not mutually exclusive by any means and almost all developers
act as users anytime they use the software.

Issues mostly suspected or confirmed **bugs**, or **enhancements**/**feature-
requests**.  Each new issue gets a unique ID (number) and the status *open*.
Developers, users and visitors can communicate back and forth.
Once the issue is resolved (bug has been fixed or ruled out, new feature has
been implemented or rejected), the issue is closed and becomes inactive.

If code is changed in response to an issue, one can (and should) cross-
reference the commit and the issue.  This can be done in two ways:
1. Add the issue ID to the commit message, e.g. `fixes: #1`, `resolves: #2`
   or `implements #3`. Some platforms can automatically close the referenced
   issue.
2. Mention one or more commit IDs (either short or long form)
   in articles of the issue. `fixed by: a1b2c3d`

Most platforms support tagging issues with custom labels. This helps
classifying them (bug, enhancement, cleanup, priority, etc.). Many allow also
to assign them to a milestone (each milestone shows the number of issues that
are still open / already closed).
Issues can also be assigned to a developer who will work on it, letting other
developers know this is going to be taken care of.

Issues are searchable by state, label, full-text, etc. ("Didn't something
similar happen 2 years ago? How exactly did we solve it?")



~~~
$ pwd
~~~
{: .language-bash}
~~~
/home/vlad/Desktop/planets
~~~
{: .output}

> ## Lorem
> Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
> tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
> quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo
> consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
> cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non
> proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
{: .callout}

{% include links.md %}
