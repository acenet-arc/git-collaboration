---
title: "Continuous Integration (CI)"
teaching: 10
exercises: 5
questions:
- "How can I run tests automatically?"
objectives:
- "Short introduction to Continuous Integration."
- "Setting up Continuous Integration for a Python project with GitHub and Travis"
- "Additional examples for GitLab-CI and Bitbucket pipelines"
keypoints:
- "Running automated tests often helps tracking down bugs early."
- "With CI tests are ran anytime changes are pushed to the repository."
- "CD automated the deployment."
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
This could mean automatically deploying code on a server whenever code has 
changed or uploading release-bundles anytime a new version is tagged --
however always under the condition that all tests are passing. 
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

These files need to contain information about all steps that are needed to 
test and optionally deploy the software.  Typical steps include:

- create a test environment
- clear or pre-populate caches
- install all dependencies
- compile the code
- run tests
- deploy code
- clean up

However not all of the steps are needed or desired in all cases.


### Example files:

Each of the CI services introduced here uses YAML as the file format 
-- a way of encoding nested lists and dictionaries --
in which the pipelines are described, however everyone uses a different set
of rules about how certain elements should be named and how they should be 
nested.  All services provide a good number of example files for several
supported languages which can be used as a starting point.

The examples below all do basically the same thing: running the unit-tests
of a Python project after installing all dependencies.
The Travis and GitLab examples run the tests with two versions of Python
(2.7 and 3.6) the Bitbucket example only tests with Python 3.6.


#### Travis-CI:
[Travis-CI tutorial][travis-turorial]
~~~
# .travis.yml
language: python
python:
  - "3.6"
  - "2.7"
# step to install dependencies
install:
  - python -V
  - "pip install -r requirements.txt"
# step to run tests
script: 
  - pytest -v
~~~
{: .language-yaml }

#### GitLab-CI:
[GitLab-CI Quickstart][gitlab-ce-ci-quickstart]
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

# .gitlab-ci.yml
test:2.7:
  image: python:2.7
  # step to install dependencies
  before_script:
    - python -V
    - pip install -r requirements.txt
  # step to run tests
  script:
    - pytest -v
~~~
{: .language-yaml }

#### Bitbucket-Pipeline:
[Getting Started with Bitbucket Pipelines][bitbucket-pipleline-getting-started]
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
>    testing_demo $  cp  more_files/.travis.yml       ./
>    testing_demo $  cp  more_files/requirements.txt  ./
>    testing_demo $  git add .travis.yml
>    testing_demo $  git commit -m "add Travis-CI config"
>    testing_demo $  git push origin master
>    ~~~
>    {: .language-bash}
> 6. Go to the "Commits tab" of your repository on GitHub.  
>    * a yellow <span style="color:orange">&#x25CF;</span> indicates testing is in progress,
>    * a green  <span style="color:green">&#x2714;</span>  indicates all tests passed.
>    * a red    <span style="color:red">&#x2716;</span>    indicates that there are failed tests,
> 7. Refresh the browser every 10 seconds until a <span style="color:red">&#x2716;</span> appears.
> 8. Click on the red <span style="color:red">&#x2716;</span> next to the latest commit,
>    and then on "Details" next to Travis-CI.
> 9. Try to fix the error in the Python code, commit and push the change 
>    and then see if the tests pass.
> 
{: .challenge}


### Other CI solutions

There are also other -- previous generation -- Build/CI/CD tools like 
[Jenkins][jenkins], that you can install on your own machine and use with 
any version control solution.  Their use however is quite different from 
the services introduced above and they are beyond the scope of this lesson.


{% include links.md %}
