---
title: "Tags and Releases"
teaching: 10
exercises: 3
questions:
- "How do you create releases of your project?"
objectives:
- "Tagging commits in the repository."
- "Creating a release."
- "Using semantic versioning."
- "Creating a DOI for a release."
keypoints:
- "Software releases add version numbers to specific states within the development cycle."
- "This is done by attaching Tags -- immutable labels -- to a certain commit."
- "Using 'Semantic Versioning' helps to communicate to a user what they can expect when upgrading."
- "Never change a release retroactively or re-release the same version with different content."
- "With Zenodo you can get a DOI for any release hosted on GitHub, making that version citable."
---

At some point you want share a certain state of the development of your software
project with other users.  At this point you will probably want to give that state
a version number, as it helps identifying the exact version a user is using when
tracking down problems.  This is referred to as "Releasing a Software" or
"Making a (Software) Release".

### Releases and Tags

Making a release of a software project that is managed by a version control
system like Git is done essentially by creating a  so called *Tag*, a name/label
that is permanently attached to specific commit to identify reference it later on.  
This can be done either using the `git tag -a <tagname>` command, and then
pushing the tag using `git push origin <tagname>` or `git push origin --tags`.

More conveniently this can also be done on the website of the repository:

* On GitHub:
  * On the main "<> Code"-tab go to the "releases"-tab.
  * Click on [Create a new release]
  * Enter a Tag version (tag-name; e.g. v0.1.0), release title (message) and
    description (release notes).
  * Make sure you are tagging the correct commit (correct branch or specific commit).
  * Optionally attach additional files (e.g. source, binary or installer packages).
    If you don't attach any files, automatic links to archives (`.tar.gz` and `.zip`)
    of the Tag's source tree are automatically generated.
  * Click [Publish Release]
* On GitLab:
  * In the menu go to Repository > Tags
  * Click on "New Tag"
  * Enter a "Tag name" (version), "Release Title" (message) and description
    (Release Notes).
  * Make sure you are tagging the correct commit (correct branch or specific commit).
  * Optionally attach additional files.  A tag's source tree can be downloaded
    on the "Tags" tab as (`.zip`, `.tar.gz` or `.tar.bz2`).
* On Bitbucket:
  * In the menu go to Commits and there on the desired commit.
  * On the right side click on the [+] "Create a tag" (next to "No tags").
  * Enter a tag-name and description.
  * Go to downloads to (optionally) add additional files.
    Any tag's source tree can be downloaded on the "Tags" tab as (`.zip`, `.tar.gz`
    or `.tar.bz2`).

The description/Release Notes can be edited later, but the tag-name and message will be immutable.

Creating a Release typically consists of the following steps:

1. **Increment the version attribute** to the desired version within the source code.
   Ideally you only have to do this in a single place, e.g. a build-script.
2. **Create a new commit** that contains the new version attribute.
   Ideally you have already committed all other changes and this commit only
   contains changes to the version attribute.
3. **Create a new Tag** which has the name of the released version and a message.  
4. **Publish Release Notes**
5. Optionally **Upload additional release files**
6. **Change the version attribute** in the source code by appending e.g. `-dev`
   and commit that change, to indicate that the source-tree is in a development state.

### Semantic Versioning

[Semantic Versioning][semver] is a versioning scheme that carries some basic
information encoded in the version number from which a user can judge how easy
or difficult it will be to upgrade to a new version.

Semantic version numbers are created with the pattern `Major.Minor.Patch` each
of them is a non-negative integer (and may have multiple digits).
Incrementing each of the numbers is done based on three rules:

1. **Major** is incremented whenever you make *incompatible changes*.
2. **Minor** is incremented whenever you make *functional changes* in a
   *backwards-compatible* way.
3. **Patch** is incremented when a release contains only *backwards-compatible fixes*.

When one of these numbers is incremented all lower-order numbers are set back to
zero.  Pre-releases or development snapshots can also have a version suffix delimited
by a dash `-`. For example:

* `X.Y.Z-dev`: A development snapshot leading up to version `X.Y.Z`
* `X.Y.Z-alpha`: An "alpha" release leading up to version `X.Y.Z`
                 intended for internal testing.
* `X.Y.Z-beta2`: The second "beta" release leading up to version `X.Y.Z`
                 intended for external testing.
* `X.Y.Z-rc1`:   The first "Release Candidate" of upcoming version `X.Y.Z`.
                 If no significant errors are found, this commit could also receive
                 the `vX.Y.Z` tag, otherwise a `-rc2` release might follow.

A special case is also the **Major version zero (0.Y.Z)** as it is used for initial
development. Anything may change at any time. The public API should not be considered
stable.

> ## Re-releasing under the same version number.
>
>  I've just yesterday released version X.Y.Z but now I've found a little bug.  
>  Can I just fix it and re-use the same version number?
>  People probably won't notice it anyway.
>
> > ## Solution:
> > ### No. Don't. Don't even think of it. NO, NO, NO!!!
> > If you have created a tag locally and haven't pushed it to a public repository,
> > you can actually do that, but otherwise this should never be done as it can
> > confuse users packagers and others later on.
> >
> > Version numbers don't cost you anything just release a new Patch release,
> > that contains only the one bugfix.
> {: .solution }
{: .discussion }

### Citable Releases (doi)

[Zenodo][zenodo] is a service that allows uploading different kinds of research
output like publications, posters, presentations, data-sets, images, video/audio
recordings, software, lessons, etc. (up to 50GB per dataset) and can issue a
Digital Object Identifier (DIO) for each published upload.  In this way you can
make each of your software releases citable -- by yourself or other users.
They can be annotated with bibliographical- (e.g. the names and ORCID of the authors),
license-, funding- and other information.

The goal for this is that publications can cite the exact versions of the used
software as well as datasets or even supplemental data, which can lead to better
reproducible research.

Zenodo is integrated with GitHub, so that you can enable GitHub repositories in
Zenodo and anytime you create a new release, it is automatically added to Zenodo,
and issued a DIO there.
If you are using a different service like GitLab or Bitbucket, you can still
upload releases manually.

> ## Be Aware:
> **Once something has been published on Zenodo, this cannot be undone!**
{: .callout}

Zenodo is funded by OpenAIRE ("Open Access Infrastructure for Research in Europe")
and data is stored in the CERN Data Center.

{% include links.md %}
