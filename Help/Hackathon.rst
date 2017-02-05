Hackathon Page
==============

This page intends to help the organisation of local hackathons. To start,
grab an invitation to our Github organization. In order to do so,
join us on coala.io/chat with your Github account and say: "Hello World". We
will then invite you. The invitation can be accepted by mail or
on https://github.com/coala.

.. note::

  This tutorial will cover basic git functionality. If, however, you have
  no prior knowledge, please consider reading
  `this link <http://api.coala.io/en/latest/Developers/Git_Basics.html>`__
  for a deeper understanding of the commands.

Running coala on a local project
--------------------------------

The first thing we plan to do is let you see coala work, for yourself.
How we plan to do this? Easily. We will simply have you run coala on a local
project of yours to see it actually do stuff. This is probably the best way
of you actually realizing what coala does.

.. note::

  If you have previously used coala and want to start contributing, you can
  skip this section.

Grabbing coala
~~~~~~~~~~~~~~

Grabbing coala is easy. Supposing you have pip installed (Python package
manager), you can simply run:

::

  pip3 install coala-bears

This will grab for you coala and all its plugins.

Using coala
~~~~~~~~~~~

Okay, so you got coala, now what? What does it do, how do I use it?

coala is a static code analysis tool. In a nutshell, it fixes/detects issues
in your code, such as syntax problems, formatting, semantic.

coala is a tool that is used by command line arguments. It requires a
configuration. So unless you have a configuration file, running ``coala`` will
not be enough. Let's see what basic arguments you can give it.

What is a bear?
A bear is a plugin which runs for a routine in your code.
As an example, we have IndentationBear which is a bear you can run to check
whether your code is indented correctly.

Let's first check if there's an existing bear for the language you have
written your project in. This can be done by running:

::

  coala --show-bears --filter-by-language C

This will list all bears available for C. You can replace "C" with your
used language. Now, supposing there are more choices of bears and you are
totally unsure what to use, simply visit
`this link <https://github.com/coala/bear-docs#all>`__
and click on each bear under your language's header. In a matter of minutes
you should decide which bear to use.


Now you are in your project's directory, have coala installed and know
what bears you want to run. Here we learn about the two core arguments that
we use to run coala: ``--files`` and ``--bears``. They are probably intuitive,
from what their names' say.

An example of a command which runs ``SpaceConsistencyBear`` on all ``C`` files
in the current directory is:

::

  coala --files=*.c --bears=SpaceConsistencyBear

Great, now coala should have yielded some results (supposing your code wasn't
perfect), and they should prompt you in the terminal and ask you for actions.
If you want to fix your code, you can give it actions (such as applying the
patches found), but for the purpose of this tutorial simply seeing coala run
should suffice.

Contributing to coala
---------------------

Now you should be here in case you have completed the first step (running
coala) or you have previously used coala.

coala uses Github and Gitlab to maintain its repositories. During this
hackathon we will only enlist the 3 most important repositories because
these have accessible issues.

coala is split in three main repositories:
 - coalib, which is the core of the coala with its libraries
 - coala-bears, which holds each bear, grouped on languages
 - documentation, which has the documentation (even this page)

To resolve an issue, you will have to locally clone the corresponding
repository and work on its code.

Picking up an Issue
~~~~~~~~~~~~~~~~~~~

Now let's pick up an issue. We use difficulty labels to mark issues, which
go from "low" to "high". Of course, for this hackathon, you will choose a
"low". In order to do so, visit coala.io/low and take a few moments to look
through the issues. You should choose one that has noone
assigned (even though in the past someone worked on it, if nobody is assigned,
feel free to take it). If it appears inactive for at least one month, you can
consider it unassigned.

.. note::

  To begin working on an issue, leave a comment that you would like to work on
  it. A maintainer will then assign you to the issue. If someone else already
  commented before you, you can assume that they are already claimed it.

If you've made it this far, you already have an issue assigned to you.
Now you gotta work on the issue. In order to do so, you should check which
repository the issue you want to work on belongs to, from the 3 repos listed
above. Clone it using:

::

  git clone https://github.com/coala/coala-bears

or the correct link corresponding to the repository. Now you'll need an online
copy of the repo (which is called a fork) which can be done by going on the
repository page and clicking on the ``Fork`` button on the top right of the
page.

Fixing the issue
~~~~~~~~~~~~~~~~

Before working on the code, you should work on a different branch than master
(so if you screw up, you still have a stable point). Use
``git checkout -b branch_name``, where ``checkout`` changes you to another
branch and ``-b`` creates a new one.

Now you're at the most challenging part. You need to fix that issue in the code
you have locally. This part cannot be contained in a tutorial as it differs
from issue to issue. Mostly, on low difficulty issues, enough information
should be given in the description or the comments of the issue. If not,
the coala maintainers present at the hackathon should probably help you as
it's your duty to ask them.

Testing your Changes
~~~~~~~~~~~~~~~~~~~~

If you have done the correct changes, you should test it. If you are working
in the ``documentation`` repository, there's nothing to be tested, but if
you aren't, you should take a look at
`this link <https://api.coala.io/en/latest/Developers/Executing_Tests.html>`__
as it shortly describes how to run our tests.

Getting the Code in the Master Branch
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now we need to create a commit. To do so, type ``git status`` and note that
the files you changed are written in red. If so, add them using ``git add``.
Once you have added all the files, type ``git commit``. This will open up
``vim`` or ``nano`` and ask you to write a commit message. In order to do so,
please read coala.io/commit, which shortly describes how to write a smart
commit message. After doing that, save it.

You cannot push to the original repository as you do not have the rights.
You will, instead, push to the fork you have created. To do that, you have
to add it locally by typing ``git remote add myfork fork_link``, where myfork
is an arbitrary name we chose. Now let's get your code up online, let's run
``git push myfork``. This will push your commit(s). You will have to request
that this code should be merged in the master branch. To do that, enter
your fork page on github.com and click on Create Pull Request. The rest
should be intuitive.

What to do after Creating a Pull Request
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Most likely your code will not be perfect. So you have to wait for review now.
Either your code will fail our checks (gitmate will point them up), or
your commit message will need work. Either way, you will receive comments
on the Github Pull Request page, and you will need to fix them.

How to fix Gitmate issues: these can be simply fixed by running ``coala``
while in the root of the project, where the ``.coafile`` file is. This will
fix all your formatting and syntax issues to your changes.

.. warning::

  If you need to change your commit, don't create another one! Edit the last
  one, as we point it out in the next lines.

To edit your commit message or fix some changes, simply do the changes to the
files, ``git add`` the files again, and this time run ``git commit --amend``.
This will edit the commit message, and, if not perfect, it can be changed
here. Then save and push again, this time with ``git push --force myfork``
as you are basically rewriting history. Now you should check that your Pull
Request has been updated.
