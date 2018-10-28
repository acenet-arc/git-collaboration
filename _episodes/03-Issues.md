---
title: "Issue Tracker"
teaching: 7
exercises: 3
questions:
- "How do I use Issues?"
objectives:
- "Filing new issues."
- "Classifying issues with labels."
keypoints:
- "Issues are used to plan further development."
- "Developers and users will communicate so that developers can reproduce bugs."
- "Enhancements and feature requests are discussed, working out the expected use-cases as well as parts of the implementation."
- "Issues of bugs and enhancements that cannot be immediately be resolved stay open so that they are not forgotten."
---

Issues are being used for communication between *users* and *developers* as
well as *developers* among themselves.

Issues mostly suspected or confirmed **bugs**, **enhancements** (feature-
requests) or **questions** on how to use a certain functionality (which in
turn might initiate improvements to the documentation).

Each new issue gets a unique ID (number) and the status *open*.

Developers, users and visitors can communicate back and forth by leaving comments.
Once the issue is resolved (bug has been fixed or ruled out, new feature has
been implemented or rejected), the issue is closed and becomes inactive.

If code is changed in response to an issue, one can (and should) cross-
reference the commit and the issue.  This can be done in two ways:
1. Add the issue ID to the commit message, e.g. `fixes: #1`, `resolves: #2`
or `implements #3`. Some platforms can automatically close the referenced
issue.
2. Mention one or more commit IDs (either short or long form)
in articles of the issue. `fixed by: a1b2c3d`

Most platforms support tagging issues with custom labels. This helps
classifying them (bug, enhancement, cleanup, priority, etc.). Many allow also
to assign them to a milestone (each milestone shows the number of issues that
are still open / already closed).
Issues can also be assigned to a developer who will work on it, letting other
developers know this is going to be taken care of.

Issues are searchable by state, label, full-text, etc. ("Didn't something
similar happen 2 years ago? How exactly did we solve it?")

> ## Create an Issue
>
> 1. Go to your `planets` repository on GitHub from the first Git workshop,
>    (or to the one of your instructor).
> 2. Switch to the *Issues* tab
> 3. Click  on _[New Issue]_
> 4. Enter a _title_ and _comment_.
> 5. Use various formatting options in the toolbar.
> 6. Use the _Preview_ tab.   
>    You can switch back and forth between the _Write_ and _Preview_ tabs
>    to test out the formatting.
> 7. Submit the issue.
>
{: .challenge}

> Most sites allow to enable/disable the issue tracker for each repository
> in the settings.  Whether it is enabled or disabled for a new repository
> depends on the default settings of the site.  Maybe you need to change
> the state in the repository's settings.
{: .callout}

{% include links.md %}
