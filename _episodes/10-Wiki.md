---
title: "Integrated Wiki"
teaching: 10
exercises: 0
questions:
- "Where can I keep some simple documentation pages?"
objectives:
- "Learn an easy way to host some documentation and/or notes."
- "Learn how to use Markdown and where to use it."
keypoints:
- "Wikis are an easy way to share simple documentation."
- "Developers can edit the documentation within the browser."
- "Permissions can be set to allow any user to edit pages."
- "This allows crowed-sourcing efforts."
- "As it is stored in a Git repository, changes can always be reverted."
- "Markdown is a lightweight and rather intuitive markup-language that is widely used."
---

Sometimes you want to keep some notes about your project and share them with
other developers and users.  While you could keep them somewhere within the 
repository, you might decide against doing so because:
- you want to navigate them easily,
- view them formatted and not as plain-text.
- don't include them in the released source packages.

The introduced services all include a Wiki functionality to do just that.

All of them support:
* Writing pages using [Markdown][markdown] which is then rendered as HTML 
  when browsing the pages.
* Pages can be edited directly on the website with a browser.
* Restrict editing to developers or allow all (registered) users.
* Show a list of all pages as well as place links on one page pointing to another.
* The Wiki is actually stored within a git-repository as well.

What are other projects using the Wiki for:

* Writing a small (maybe preliminary) User's manual.
* Maintaining a Developer's Manual
    * steps to create a development environment
    * commands to build the project
    * style guide
    * Whitepaper
* Showcase of usage

### Markdown primer

[Markdown][markdown] is a lightweight markup-language that looks intuitively 
nice when viewed as plain-text and renders nicely as HTML with things like
bullet- and numbered lists, several levels of headings, sub-headings, sub-sub-
headings (etc.), links, included images, code blocks, etc.

These services have expanded the original Markdown specification by additional
elements like:
* code-blocks with syntax-highlighting for very many languages
* linking to issues, pull-requests, commits, files, lines in files, branches, etc.
* tables

While they often follow the same syntax rules but sometimes differ slightly
-- especially when it comes to placing links to site features like pull-requests.

Therefore each site has a guide to their own Markdown flavor:

* [GitHub Flavored Markdown][github-markdown]
* [GitLab Flavored Markdown][gitlab-markdown]
* [Bitbucket Markdown][bitbucket-markdown]

The sites not only render Markdown within the Wiki but also in comments, 
issues, pull-requests, code-review, release-notes, etc. as well as 
files with the `*.md` and `.markdown` file extension.



#### A few Markdown examples:

<div class="row">
  <div class="col-md-6" markdown="1">
~~~
format words in **bold** or *italics*

use `inline code` markup
~~~
{: .source}
  </div>
  <div class="col-md-6" markdown="1">
format words in **bold** or *italics*

use `inline code` markup
  </div>
</div>


<div class="row">
  <div class="col-md-6" markdown="1">
~~~
*   Use asterisks
*   to create
*   bullet lists.
~~~
{: .source}
  </div>
  <div class="col-md-6" markdown="1">
*   Use asterisks
*   to create
*   bullet lists.
  </div>
</div>

<div class="row">
  <div class="col-md-6" markdown="1">
~~~
1.  Use numbers
1.  to create
1.  numbered lists.
~~~
{: .source}
  </div>
  <div class="col-md-6" markdown="1">
1.  Use numbers
1.  to create
1.  numbered lists.
  </div>
</div>

<div class="row">
  <div class="col-md-6" markdown="1">
~~~
*  You can use indents
	*  To create sublists 
	*  of the same type
*  Or sublists
	1. Of different
	1. types
~~~
{: .source}
  </div>
  <div class="col-md-6" markdown="1">
*  You can use indents
	*  To create sublists
	*  of the same type
*  Or sublists
	1. Of different
	1. types
  </div>
</div>

<div class="row">
  <div class="col-md-6" markdown="1">
~~~
# A Level-1 Heading
~~~
{: .source}
  </div>
  <div class="col-md-6" markdown="1">
# A Level-1 Heading
  </div>
</div>

<div class="row">
  <div class="col-md-6" markdown="1">
~~~
## A Level-2 Heading (etc.)
~~~
{: .source}
  </div>
  <div class="col-md-6" markdown="1">
## A Level-2 Heading (etc.)
  </div>
</div>

<div class="row">
  <div class="col-md-6" markdown="1">
~~~
Line breaks
don't matter.

But blank lines
create new paragraphs.
~~~
{: .source}
  </div>
  <div class="col-md-6" markdown="1">
Line breaks
don't matter.

But blank lines
create new paragraphs.
  </div>
</div>

<div class="row">
  <div class="col-md-6" markdown="1">
~~~
[Create links](http://software-carpentry.org) with `[...](...)`.
Or use [named links][data_carpentry].

[data_carpentry]: http://datacarpentry.org
~~~
{: .source}
  </div>
  <div class="col-md-6" markdown="1">
[Create links](http://software-carpentry.org) with `[...](...)`.
Or use [named links][data_carpentry].

[data_carpentry]: http://datacarpentry.org
  </div>
</div>

<div class="row">
  <div class="col-md-6" markdown="1">
~~~
Insert images with `![alt-text](URL)`:
![Git Logo](https://git-scm.com/images/logo.png) 
~~~
{: .source}
  </div>
  <div class="col-md-6" markdown="1">
Insert images with `![alt-text](URL)`:
![Git Logo](https://git-scm.com/images/logo.png) 
  </div>
</div>

<div class="row">
  <div class="col-md-6" markdown="1">
~~~
A python code-block:
```python
def square(x):
    return x * x
```
Many other languages are supported.
Just change `python` into something else.
~~~
{: .source}
  </div>
  <div class="col-md-6" markdown="1">
A python code-block:
```python
def square(x):
    return x * x
```
Many other languages are supported. 
Just change `python` into something else.
  </div>
</div>


Most of these examples are taken from:
[Software Carpentry: Plotting and Programming in Python][python-gapminder]
2016.

{% include links.md %}
