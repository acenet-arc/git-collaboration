---
title: "Introduction"
teaching: 5
exercises: 5
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
{% include mermaid.html %}
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
