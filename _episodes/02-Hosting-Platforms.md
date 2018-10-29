---
title: "Overview of Git hosting sites"
teaching: 15
exercises: 0
questions:
- "What are the most-widely used Git hosting sites?"
objectives:
- "Common functionalities of Git Hosting sites."
- "What are some of the differences."
keypoints:
- "Several services exist that offer hosting of Git repositories."
- "Hosting of public and/or Open-Source projects is mostly free of charge."
- "Hosting of non-public repositories often requires a paid-for plan or has certain restrictions."
- "Several self-hosted solutions exist."
---

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
#### [GitHub][github]
* Biggest site
* Private repositories for a fee
* Free packages for Students, Teachers/Educators
* Hosting of static websites (GitHub pages)
* external Continuous Integration service: Travis-CI.com
* integrated with many 3rd party services

#### [Bitbucket][bitbucket]
* Supports also Mercurial (`hg`) repositories
* Free private repositories (max 5 collaborators)
* Academic accounts (User and/or Team) with unlimited private repositories.

#### [GitLab.com][gitlab]
* Free private repositories
* Hosting of static websites (GitLab pages)

#### Others:
* SourceForge.net
* Google Code (closed)

### Self-Hosted
* Run a Git Hosting Platform on your own server.

#### [GitLab Community Edition (CE)][gitlab-ce]
* Open Source version of the software running on GitLab.com
* Almost all features of GitLab.com

#### [Gitea][gitea]
* Very lightweight but just the basic features

#### Others:
* [Trac](https://trac.edgewall.org/)
* [Gogs](https://gogs.io/)
* [gitolite](http://gitolite.com/) (only repository - no other features)

{% include links.md %}
