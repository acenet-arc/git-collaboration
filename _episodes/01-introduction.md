---
title: "Introduction"
teaching: 10
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- 'Review important points from the lesson "Version Control with Git".'
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
{% include mermaid.html %}

## Recap: Important Git commands

1. `git config` - configure personalized settings for Git.
1. `git init`   - initializes a new Git-repository.
1. `git status` - shows the status of the repository.
1. `git add`    - adds a file to the staging area.
1. `git commit` - store staged changes as a new change-set (commit).
1. `git diff`   - show differences between versions. By default the difference 
                  between working directory and staging area.
1. `git log`    - shows list of versions (commits).
1. `git checkout` - recover old versions of files and switch branches.
1. `git remote` - adds or changes the location of the remote report.
1. `git push`   - copy commits from local repository to remote repository.
1. `git pull`   - copy commits from remote repository to local repository (fetch)
                  and integrate (merge) them into working directory.
1. `git clone`  - creates a local copy of a remote repository.

## Recap: the Git working Cycle

### Working locally
<div class="mermaid">
graph TD
  A[ git init ] -- creates new repository -->  C ;
  C([create and edit files]) --> D ;
  D[ git add ]  -- adds files to staging area --> E ;
  E[ git commit ] -- commits changes to local repository --> G ;
  G([working directory clean]) ----> C;
</div>

### Typical workday with remote repository

<div class="mermaid">
graph TD
  A{start} --> B ;
  B[ git pull ] -- retrieve changes from remote --> C ;
  C([create and edit files]) --> D ;
  D[ git add ]  -- adds files to staging area --> E ;
  E[ git commit ] -- commits changes to local repository --> F ;
  F[ git push ] -- push commits to remote repository --> G ;
  G([working directory clean]) --> H{end of day}; 
  E -- continue working --> C ;
  G -- continue working --> C ;
  H -- new day --> A ;
</div>

{% include links.md %}
