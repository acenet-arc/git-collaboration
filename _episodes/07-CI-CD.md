---
title: "Continuous Integration (CI)"
teaching: 10
exercises: 0
questions:
- "How can I run tests automatically? (FIXME)"
objectives:
- "Setting up Continuous Integration for a Python project with GitHub and Travis"
- 
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---

Devising a number of automated tests that are testing all "bits of code"
if everything is working correctly -- called Unit Tests -- has become 
a good practice in software development.

But having a large set-suite is only helpful when you run it in it's entirety 
on a regular basis. Otherwise you risk to miss side-effects of your changes
for too long and it becomes more difficult to track down which change caused
the test(s) to brake when there have been too many changes since the test 
was last used.

The practice that is designed of helping with that is called **Continuous Integration**
and is abbreviated as **CI**. CI automates building and/or running a test-suite 
whenever changes are pushed to the repository on the server or whenever a 
Pull-Request is opened.

Continuous Integration is often combined with **Continuous Delivery (CD)**, 
where changes to a software are put into production either fully automatically,
once all tests have passed, or semi-automatically where a designated developer
just has to trigger the otherwise fully-automatic roll-out.
Together they are commonly referred to as a **CI/CD Pipeline**.

For GitHub there is an external service called [Travis-CI][travis], 
GitLab and Bitbucket have CI/CD-pipelines directly build-in.
All of those services count the number of minutes these pipelines run on their 
servers and have different restrictions on how long the service can be used
for free and from which point a project has to pay:

* Travis-CI offers unlimited pipeline minutes for free for public repositories,
  while they charge for building/testing private repositories.
* GitLab.com's free plan includes 2,000 CI pipeline minutes per group per month.
* Bitbucket's free plan includes 50 pipeline minutes per month and their 
  Academic plan includes 500 free minutes per month.

(as of October 2018)

GitLab also allows to use your own GitLab runners that are running on your
computer. 

These three CI-pipeline services have in common that they are configured
with a single text file in the [YAML][yaml] format, which is placed in the
root directory of a project under a specific name: `.travis.yml` for Travis-CI,
`.gitlab-ci.yml` for GitLab and `bitbucket-pipelines.yml` for Bitbucket.

### Examples:

~~~
# .travis.yml
language: python
python:
  - "2.7"
  - "3.6"
# step to install dependencies
install:
  - python -V
  - "pip install -r requirements.txt"
# step to run tests
script: 
  - pytest -v
~~~
{: .language-yaml }

~~~
# .gitlab-ci.yml
test:3.6:
  image: python:3.6
  # step to install dependencies
  before_script:
    - python -V
    - pip install -r requirements.txt
  # step to run tests
  script:
    - pytest -v
~~~
{: .language-yaml }

~~~
# bitbucket-pipelines.yml
image: python:3.6
pipelines:
  default:
    # step to install dependencies
    - step:
        name: install dependencies
        caches:
          - pip
        script:
          - python -V
          - pip install -r requirements.txt
    # step to run all tests
    - step:
        name: run all tests
        script:
          - pytest -v
~~~
{: .language-yaml }

> ## Getting Started with GitHub and Travis-CI
> 1. Go to [Travis-ci.com][travis] and Sign up with GitHub.
> 2. Accept the Authorization of Travis CI. You’ll be redirected to GitHub.
> 3. Click the green Activate button, and select the repositories you want to use with Travis CI.
> 4. Co to the cloned `testing_demo` repository on your computer.
> 5. Copy the prepared `more_files/.travis.yml` file into the root directory,
>    then commit the change and push to GitHub:
>    ~~~
>    testing_demo $  cp more_files/.travis.yml   ./
>    testing_demo $  git add .travis.yml
>    testing_demo $  git commit -m "add Travis-CI config"
>    testing_demo $  git push origin master
>    ~~~
>    {: .language-bash}
> 6. Go to the "Commits tab" of your repository on GitHub. Maybe you need reload 
>    after 20 seconds until a <span style="color:red">&#x2718;</span> appears.
> 7. Click on the red <span style="color:red">&#x2718;</span> next to the latest commit,
>    and then on "Details" next to Travis-CI
> 
{: .challenge}


### Other solutions

There are also other -- previous generation -- Build/CI/CD tools like 
[Jenkins][jenkins], that you can install on your own machine and use with 
any version control solution.  Their use however is quite different from 
the services introduced above and they are beyond the scope of this lesson.


[travis-turorial]: https://docs.travis-ci.com/user/tutorial/
[gitlab-ce-ci-quickstart]: https://docs.gitlab.com/ce/ci/quick_start/README.html
[bitbucket-pipleline-getting-started]: https://confluence.atlassian.com/bitbucket/get-started-with-bitbucket-pipelines-792298921.html


{% include links.md %}
