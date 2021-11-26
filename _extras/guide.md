---
title: "Instructor Notes"
---
{% include mermaid.html %}

This a transcript how this repository is used alongside the
[Git Collaboration]({{ site.baseurl }}) lesson.

In a workshop
* the the instructor forks the original (template) testing_demo repository and
* the workshop attendees will fork the instructor’s fork of the testing_demo repository.

In the end, the fork-tree should look something like this for a workshop with five attendees:

<div class="mermaid">
flowchart RL
  A( acenet-arc /<br />testing_demo ) ;
  B[ instructor /<br /> testing_demo ] -- fork of --> A ;
  subgraph Used in the workshop
  C1[ attendee1 /<br /> testing_demo ] -- fork of --> B ;
  C2[ attendee2 /<br /> testing_demo ] -- fork of --> B ;
  C3[ attendee3 /<br /> testing_demo ] -- fork of --> B ;
  C4[ attendee4 /<br /> testing_demo ] -- fork of --> B ;
  C5[ attendee5 /<br /> testing_demo ] -- fork of --> B ;
  end
</div>

The original repository will remain in its initial state and issues and pull-requests
will only be created towards the instructor’s fork of the repository.

### 1. Introduction

This episode includes only a short recap on the Git workflow.

### 2. Overview of Git hosting sites

This episode gives an overview over the Git Hosting Platforms GitHub, GitLab.com
and Bitbucket.

### 3. Issue Tracker

FIXME

### 4. Forking a Repository

In the episode [Forking a Repository]({{ site.baseurl }}/04-Forking/)
the instructor will fork the (template) testing_demo repository and the the workshop attendees will
fork the instructor’s fork of the testing_demo repository.

### 5. Pull Requests

In the episode [Pull Requests]({{ site.baseurl }}/05-Pull-Requests)
a change will be committed to the forked repository and for this change a "pull request"
(by some platforms also called "merge request") will be opened towards the *instructor's* copy
of the repository.

The commands are in the call-out box
[Submit a Pull Request]({{ site.baseurl }}/05-Pull-Requests/#submit-a-pull-request) within the episode.

### 6. Code Review

In the episode [Code Review]({{ site.baseurl }}/06-Code-Review) the previously opened pull-request
is used to conduct a code-review. Attendees work in pairs and review each others pull-requests.
This is all done on the website.

### 7. Continuous Integration (CI)

In the episode [Continuous Integration]({{ site.baseurl }}/07-CI-CD) prepared workflow files are used
to enable Continuous Integration pipelines.

The commands are in the call-out box [Getting Started with GitHub Actions]({{ site.baseurl }}/07-CI-CD/#getting-started-with-github-actions-1)

### 8. Tags and Releases

In the episode [Tags and Releases]({{ site.baseurl }}/08-Tags-Releases/) a release (and the
accompanying tag) are created on the repository's website.
Also the topics of semantic versioning and citable releases are discussed.

### 9. Branches

The episode [Branckes]({{ site.baseurl}}/09-Branches/) introduces the concept of branches and uses
the [Git Sandbox][learnGitSandbox] to practice the different commands.

### 10. Integrated Wiki

The episode [Integrated Wiki]({{ site.baseurl}}/10-Wiki/) introduces the Markdown syntax
and how to use it on the Wiki modules that are integrated into the platforms.

### 11. Pages

The episode [Pages]({{ site.baseurl}}/11-Pages/) shows how to host a static website with GitHub
Pages and gives pointers how to do the same with GitLab pages and Bitbucket.

{% include links.md %}
