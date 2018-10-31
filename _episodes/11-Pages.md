---
title: "Pages"
teaching: 10
exercises: 5
questions:
- "How can I host a simple website?"
objectives:
- "Learn how to host a static website with documentation or a blog on a Git Platform."
keypoints:
- "GitHub, GitLab and Bitbucket offer a way hosting a website on their platform."
- "The pages are stored in a Git repository."
- "The pages are static in a sense that there are no server-side scripts or databases."
- "GitHub and GitLab offer building pages from e.g. Markdown files with 'Jekyll'"
- "In those cases Jekyll is executed whenever commits are pushed to the server."
- "The process works like a CI/CD pipeline."
---

Sometimes hosting a few simple Wiki pages is not sufficient for a project
and you want to host a small website using your own design or an amount of 
content that exceeds the capabilities of Wiki pages.

GitHub, GitLab.com and Bitbucket offer hosting pages directly from a Git repository.
Whey you create a repository with the name `<username>.github.io`, the content 
of that repository will be available under "https://<username>.github.io".
Other repositories can be set serve pages under "https://<username>.github.io/<reponame>".

The same methodology applies to GitLab and Bitbucket with the `<username>.gitlab.io`
and `<username>.bitbucket.io` domains respectively.  GitHub and GitLab also 
allow configuring a custom domain, e.g. `www.example.com`.


### Deploying a page with GitHub pages

Let's try out serving a small page on GitHub from within your `testing_demo`
repository.

First we need to activate the "Pages" functionality for this repo:

1. go to the repository's settings, 
2. scroll down to "GitHub Pages"
3. in the dropdown select **master branch / docs folder**
4. click **Save**
5. we **don't** use the Theme Chooser at this point.

Now we go back to our checked out repository:

~~~
testing_demo $  git pull origin
testing_demo $  mkdir docs
testing_demo $  cd  docs
~~~
{: .language-bash }

In the docs directory we first create a file `_config.yml` with the following
content:

```yaml
# _config.yml
# Jekyll configuration
name:  My Cool Page
title: My Cool Page
description: A Documentation Page created with Jekyll
theme: jekyll-theme-architect
```

Next we create a file `index.md` with some Markdown content:

```markdown
<!-- index.md -->
# My Testing Docs Page

It Works! :-)

1. Have a `_config.yml` file setting a `title`, `name`, `description` and `theme`.
2. Add an `index.md` file with the landing page in Markdown.
3. Add more `*.md` files, e.g. `about.md`
4. add a link to [about.md](about) with: `[about.md](about)`
```

Now we commit the changes and push them to GitHub:

~~~
testing_demo $  git add _config.yml index.md
testing_demo $  git commit -m "my first GitHub page"
testing_demo $  git push origin master
~~~
{: .language-bash }

Switch back to the browser and reload the settings page.  Under the GitHub
pages section you should now see the URL under which the site was published
(`https://<username>.github.io/testing_demo/`).  Click on that link -- et viol&agrave;!

From the data inside the [Jekyll][jekyll] configuration file `_config.yml` 
and landing page `index.md` in Markdown format, a website was build on
the GitHub servers and is now available to be viewed by anyone.


> ## Change the Jekyll theme
> 
> Go back to the repository's settings and use the *Theme Chooser* to select
> a different theme.  
> Notice that this has generated a new commit.  Use `git pull origin` to pull
> this change into your local repository.
>
{: .challenge }



> ## Some notes on GitHub pages
>
> * In this example the web-pages are located in a `docs` sub-directory within 
>   the repository.  We could have placed the `_config.yml`, `index.md` and
>   other files instead into the repository's root directory  of the `master`
>   or `gh-pages` branch and selected the appropriate option from the dropdown
>   in the repository's GitHub-pages settings.
>
> * Previously GitHub pages had to be hosted from a branch called `gh-pages`.
>   This could have been the sole branch of a repository or in addition to
>   a `master` branch with code.  This is still possible but no longer a requirement.
> 
{: .callout }


### GitLab pages

[GitLab Pages][gl-pages] makes use of the [GitLab CI][gitlab].  This makes
the GitLab pages a bit more flexible but in turn you must maintain your
`.gitlab-ci.yml` pipeline definition yourself.
However there are a number of examples for different use-cases that can 
be easily adapted.


### Bitbucket pages

At the time this material is being created (October 2018), Bitbucket
only serves HTML-pages as they are directly from the repository.

Please consult their [documentation][bb-pages] for more information
and features that have been introduced since then.


Documentation:
* [GitHub Pages][gh-pages]
* [GitLab Pages][gl-pages]
* [Bitbucket Pages][bb-pages]




{% include links.md %}
