---
title: "Continuous Integration (CI)"
teaching: 15
exercises: 10
questions:
- "How can I run tests automatically?"
objectives:
- "Short introduction to Continuous Integration."
- "Setting up Continuous Integration for a Python project with GitHub and Travis"
- "Additional examples for GitLab-CI and Bitbucket pipelines"
keypoints:
- "Running automated tests often helps tracking down bugs early."
- "With CI, tests are being executed anytime changes are pushed to the repository."
- "CD is used to automate the deployment of new releases."
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
This could either mean automatically deploying code on a server whenever code has 
changed or packaging and uploading uploading release-bundles anytime a new version is tagged --
however always under the condition that all tests are passing.  
Together they are commonly referred to as a **CI/CD Pipeline**.

The three major Git-Hosting websites have CI/CD-pipelines directly build-in:
[GitHub Actions][gh-actions], [GitLab-CI][gl-ce-ci] and 
[Bitbucket Pipelines][bb-piplelines] and besides that there are also external
services like [Travis-CI][travis] and [Circle-CI][circle-ci].

All of those services count the number of minutes these pipelines run on their 
servers and have different restrictions on how long the service can be used
for free and from which point a project has to pay:

* GitHub Actions's free plan includes 2,000 pipeline minutes/month for public
  repositories.
* GitLab.com's free plan includes 400 CI pipeline minutes per group per month.
* Bitbucket's free plan includes 50 pipeline minutes per month and their 
  Academic plan includes 500 free minutes per month.

(as of October 2021)

Both GitHub and GitLab also allow you to use your own GitLab runners that are
running on your computer. Using private runners is free of charge and the
minutes that these runners are working are not billed.

These three CI-pipeline services have in common that they are configured
with a single text file in the [YAML][yaml] format, which for GitHub Actions
is placed in a directory called `.github/workflows` and for other services into
root directory of a project the a specific name: 
`.gitlab-ci.yml` for GitLab, `bitbucket-pipelines.yml` for Bitbucket and 
`.travis.yml` for Travis-CI,.

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
(2.7 and 3.8) the Bitbucket example only tests with Python 3.8.


#### GitHub Actions:
[GitHub Actions Quickstart][gh-actions-quickstart]
{% raw %}
~~~
# .github/workflows/github-actions.yml
name: learn-github-actions
on: [push]
jobs:
  test-my-python-code:
    # select the os-image these jobs should run on
    runs-on: ubuntu-latest
    
    # define the Python versions that should be used
    strategy:
      matrix:
        python-version: [2.7, 3.8]

    steps:
      # step to check out the repository
      - uses: actions/checkout@v2

      # step to create the Python environment
      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v2
        with:
          python-version: ${{ matrix.python-version }}

      # step to install the dependencies
      - name: Install dependencies
        run: "pip install -r requirements.txt"

      # step to run tests
      - run: pytest -v
~~~
{: .language-yaml }
{% endraw %}


#### GitLab-CI:
[GitLab-CI Quickstart][gitlab-ce-ci-quickstart]
~~~
# ./.gitlab-ci.yml
test:2.7:
  image: python:2.7
  # step to install dependencies
  before_script:
    - python -V
    - pip install -r requirements.txt
  # step to run tests
  script:
    - pytest -v

test:3.8:
  image: python:3.8
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
# ./bitbucket-pipelines.yml
image: python:3.8
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

### Getting Started with GitHub Actions

Let's get our feet wet with GitHub Actions.

> ## Getting Started with GitHub Actions
> 1. Go to the cloned `testing_demo` repository on your computer.
> 2. Create the `.github` and `.github/workflows` directories:
>    ~~~
>    mkdir .github
>    mkdir .github/workflows
>    ~~~
>    {: .language-bash}
> 5. Copy the prepared `more_files/github-actions.yml` file to the 
>    `.github/workflows` directory, as well as the `requirements.txt` to the root,
>    then commit the change and push to GitHub:
>    ~~~
>    testing_demo $  cp  more_files/github-actions.yml  .github/workflows
>    testing_demo $  cp  more_files/requirements.txt  ./
>    testing_demo $  git add .github/workflows
>    testing_demo $  git add requirements.txt
>    testing_demo $  git commit -m "add GitHub Actions"
>    testing_demo $  git push origin main
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


### A Second Look at the Pipeline definitions

Let's have another look at the pipeline definitions to see what they are actually doing.

#### GitHub Actions revisited:

Let's go over this workflow line by line:
{% raw %}
~~~
name: learn-github-actions
on: [push]
jobs:
  test-my-python-code:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [2.7, 3.8]

    steps:
      - uses: actions/checkout@v2

      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v2
        with:
          python-version: ${{ matrix.python-version }}

      - name: Install dependencies
        run: "pip install -r requirements.txt"

      - run: pytest -v
~~~
{: .language-yaml }
{% endraw %}


*  This line defines the name of the workflow and will appear in the 'Actions' tab of the GitHub 
   repository.
  ~~~yaml
  name: learn-github-actions
  ~~~

* This line specifies that this workflow should be executed whenever commits are pushed to the 
  repository (a "push-event"). It is possible to set the pipeline to only run for pull-requests or 
  to only run the workflow only on certain branches or paths or tags. 
  See: [Workflow syntax for GitHub Actions][gh-actions-onpush] for more information.
  ~~~yaml
  on: [push]
  ~~~

* An event (like a push) triggers the workflow that can consist of one or more jobs and each job can 
  consist of one or more steps, for example:
  ~~~yaml
  jobs:
    job1:
      steps:
        - run:  command
        - run:  command
    job2:
      steps:
        - run:  command
        - run:  command
  ~~~
  Also the name for each job can be defined, e.g. `job1` and `job2` or something more descriptive
  like `test-my-python-code`.
  ~~~yaml
  jobs:
    test-my-python-code:
      steps:
        - run:  command
        - run:  command
  ~~~

* This configures the job to run on an Ubuntu Linux runner. Other operating systems and versions 
  are available as well.  Each job will run on a fresh virtual machine (or container). 
  See [Workflow syntax for GitHub Actions][gh-actions-runson] for more information.
  ~~~yaml
  runs-on: ubuntu-latest
  ~~~

* These lines define that this job should be executed multiple times with two different Python 
  versions, 2.7 and 3.8. 
  The test matrix could also involve  multiple operating systems (e.g. Linux, Windows, macOS), 
  however keep in mind that testing with  e.g. three  python-versions on three different operating 
  systems already generates 9 jobs. 
  Running all of these on every commit can quickly deplete the available pipeline-minutes.
  ~~~yaml
  strategy:
    matrix:
      python-version: [2.7, 3.8]
  ~~~
  
* This contains a list of steps that should be executed within the job. Let's look at 
  the four steps and start with the simplest:
  {% raw %}
  ~~~yaml
  steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-python@v2
    - run:  pip install -r requirements.txt
    - run:  pytest
  ~~~
  {% endraw %}
  
  * This step just runs the command `pytest`.  That wasn't too hard, was it?
    {% raw %}
    ~~~yaml
      - run:  pytest -v
    ~~~
    {% endraw %}

  * Next we have a step consisting of two lines. The second line runs a `pip install` commands to
    install the required Python packages defined in the `requirements.txt` file.  The first line
    defines a name for this step that will show up in the pipeline logs.  If we would not define
    the name, this step would show up as "Run pip install -r requirements.txt".
    {% raw %}
    ~~~yaml
    - name: Install dependencies
      run: "pip install -r requirements.txt"
    ~~~
    {% endraw %}

  * This step doesn't execute a simple shell command, but rather calls an external "action" 
    with the name "action/checkout" in its version "v2" (this is the version of the action, not
    of our code!). 
    This action will checkout the current git repository so that the tests can be executed.  
    Details for this action can be found at: [github.com/actions/checkout][gh-actions-checkout]
    {% raw %}
    ~~~yaml
    - uses: actions/checkout@v2
    ~~~
    {% endraw %}


  * The following lines will also use an "action", this time [actions/setup-python@v2][gh-actions-setuppython],
    which creates a Python environment for a particular Python version.  The lines `with:` > 
    `python-version: ${{ matrix.python-version }}`
    will set the variable `python-version` that is used by the `setup-python` action to the current 
    value of `matrix.python-version` from  our test-matrix.  
    Finally this step also defines a name that includes the Python version from the variable.
    {% raw %}
    ~~~yaml
      - name: Set up Python ${{ matrix.python-version }};
        uses: actions/setup-python@v2
        with:
          python-version: ${{ matrix.python-version }}
    ~~~
    {: .language-yaml }
    {% endraw %}

#### GitLab-CI revisited
FIXME: GitLab-CI revisited

#### Bitbucket-Pipeline revisited
FIXME: Bitbucket-Pipeline revisited

### Other CI solutions

There are also other Build/CI/CD services and tools that can be use as an 
alternative to those provided by the Git-Hosting services.

The cloud services [Travis-CI][travis] and [Circle-CI][circle-ci] work similar 
to the methods described above, in that they are also controlled by [YAML][yaml] 
files that are added to the repositories. The only additional steps that are needed 
is to sign up for an account with the service and to link the cloud-service to the 
repository in the project's settings menu under "Integrations".

[Jenkins][jenkins] and other similar tools, been around much longer than the services described 
above, and it requires that you can install on your own machine and can be used with any version 
control solution.  Running the pipelines can then either be triggered by web-hooks (the Source code
repository calls a certain URL when a new commit has been pushed) or on a defined schedule (cron-job).
Jenkins also doesn't use [YAML][yaml] to describe the pipelines, but has its own "Domain Specific 
Language" for it's `Jenkinsfile`s.
Also in terms of their use however is quite different from the services introduced above and they 
are beyond the scope of this lesson.

{% include links.md %}
