---
title: "Overview of Git hosting sites"
teaching: 15
exercises: 0
questions:
- "What are the most-widely used Git hosting sites?"
objectives:
- "Common functionalities of Git Hosting sites."
- "Differences between Git hosting sites."
keypoints:
- "Several services exist that offer hosting of Git repositories."
- "Hosting of public and/or Open-Source projects is mostly free of charge."
- "Hosting of non-public repositories often requires a paid-for plan or has certain restrictions."
- "Several self-hosted solutions exist."
---

* Many common features:
  * Usually free for public and private repositories
  * Private repositories may have some limitations
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
    * Organizations (GH), Groups (GL), Teams/Projects (BB)
  * Snippets (GitHub: Gist)
  * Continuous Integration (CI, Pipelines)
    * limited number of CI-minutes per month for free

## Hosted Platforms

Note that the providers below are constantly adding new features and the list below 
is just a snapshot of notable features at the time of writing and does not claim
to be complete in any way but should just serve as a limited overview.

### [GitHub][github]

* Biggest site
* Unlimited public/private repositories
* Hosting of static websites using [GitHub pages](https://docs.github.com/en/pages)
* Continuous Integration ([GitHub Actions](https://docs.github.com/en/actions)):
  * free CI-minutes for public repositories and self-hosted runners
  * limited free monthly CI-minutes for private repositories
* Package registry ([GitHub Packages](https://docs.github.com/en/packages))
  * host packages for npm, RubyGems, Maven, Gradle, NuGet, Container
  * free for public packages
  * certain amount of free storage and data transfer for private packages
* GitHub sends "Dependabot" alerts for vulnerable dependencies
* Integrated with many 3rd party services
* Offers for Students, Teachers/Educators, OpenSource Teams, Nonprofits.

### [GitLab.com][gitlab]

* Unlimited public/private repositories
* Hosting of static websites using [GitLab pages](https://docs.gitlab.com/ee/user/project/pages/)
* Continuous Integration ([CI/CD pipeline](https://docs.gitlab.com/ee/ci/)) 
  with limited free monthly CI-minutes
* [Package registry](https://docs.gitlab.com/ee/user/packages)
  * Host packages for npm, Maven, NuGet, PyPI, Containers
  * Support for other types is available as _Beta_
  * Limited repository storage amount per project is free
* Additional CI/CD minutes and package storage can be purchased

### [Bitbucket][bitbucket]

* Unlimited public/private repositories (max 5 collaborators)
* Academic accounts (User and/or Team) with unlimited private repositories.
* Continuous Integration ([CI/CD pipeline](https://bitbucket.org/product/features/pipelines)) 
  limited free monthly CI-minutes

### Others

* SourceForge.net
* Google Code (closed)

## Self-Hosted

* Run a Git Hosting Platform on your own server.

### [GitLab Community Edition (CE)][gitlab-ce]

* Open Source version of the software running on GitLab.com
* Almost all features of GitLab.com

### [Gitea][gitea]

* Very lightweight but just the basic features

### Others

* [Trac](https://trac.edgewall.org/)
* [Gogs](https://gogs.io/)
* [gitolite](http://gitolite.com/) (only repository - no other features)

{% include links.md %}
