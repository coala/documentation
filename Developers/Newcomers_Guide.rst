.. _newcomer-guide:

Welcome to the Newcomers Guide!
===============================

This is a step-based guide that will help you get your first contribution
at coala!

Step 1. Meet the Community!
---------------------------

To get started, the first step is to meet the community. We use gitter to
communicate, and there the helpful community will guide you.
Join us at `coala gitter <https://gitter.im/coala-analyzer/coala/>`_.
The newcomers should ping us "Hello World" to let us know they are here
because we care!

**Congratulations!** You are now part of our community.

Step 2. Grab an Invitation to the Organization
----------------------------------------------

Let us know on gitter that you are interested in contributing and ask for an
invitation to our org. This is your first step towards contributing.
The invitation will be sent by mail and you will have to accept
it to join. If you don't find the invitation, accept it `here <https://github.com/coala-analyzer>`_.

Now that you are part of our organization, you can start working on issues.
If you are familiar with git, you can skip the next section and pick an issue.

Optional. Get Help With Git
---------------------------

We use GitHub to manage our repository. If you're not familiar with git, we
strongly recommend following a tutorial, such as `this one <https://try.github.io/levels/1/challenges/1>`_.

We also have a page dedicated to git commands that will help you learn the
basics,
:doc:`here <Git_Basics>`.

If there's anything unclear, or you are encountering problems, feel free
to contact us on `gitter <https://gitter.im/coala-analyzer/coala/>`_,
and we will help you!

Step 3. Picking Up an Issue
---------------------------

Now it is time to pick an issue.
Here is the link that will lead you to `Newcomers issues <https://coala.io/new>`_.

.. seealso::

    For more information about what bears are, please check the following link: `Writing bears <http://coala.io/writingbears>`_

The easy issues that will help you get started are labeled as
``difficulty/newcomer`` and are only there to give you a glimpse of how it is
to work with us and regarding the workflow.

Now pick an issue which isn't assigned, and if you want to fix
it, then leave a comment that you would like to get assigned. This way
we don't have multiple people working on the same issue at the same time.
Now you can start working on it.

.. note::

    Before starting to write your first commit, check out this link:
    :doc:`Writing good commits <Writing_Good_Commits>`.

Step 4. Creating a Fork and Testing Your Changes
------------------------------------------------

This tutorial implies you working on your fork. To fork the repository, go
to the official repository of coala/coala-bears and click on the ``Fork``
button from the website interface. To add it locally, simply run:

::

    $ git remote add myfork fork_link

where ``myfork`` is the name of your fork, and ``fork_link`` is a link to your
fork repository.

Now you need to make sure your change is actually working. For this, you will
need to test it locally before pushing it to your fork, and checking it with
concrete examples. So basically, run tests and run coala by simply typing

::

    $ coala

into your bash. This will analyze your code and help you fix it.

.. seealso::

    `Executing tests <http://coala.readthedocs.org/en/latest/Getting_Involved/Testing.html>`_

Step 5. Sending Your Changes
----------------------------

Now that you've fixed the issue, you've tested it and you think it is ready
to be merged, create a commit and push it to your fork, using:

::

    $ git push myfork

where ``myfork`` is the name of your fork that you added at the previous step.

.. note::

    You could also add a profile picture on your Github account, so that you can be
    distinguished out from the crowd!

Step 6. Creating a ``Pull Request``
-----------------------------------

Now that your commit has been sent to your fork, it is time
to do a ``Pull Request``. It can be done by accessing your fork on GitHub and
clicking ``New Pull Request``.

**Congratulations!** You have now created your first ``Pull Request``!

If you know you have more work to do on this ``Pull Request`` before it is
ready to be accepted, you can optionally indicate this to other
developers by starting your ``Pull Request`` title with ``wip``
(case-insensitive).

Step 7. Review Process
----------------------

After creating your ``Pull Request``, it is under the review process. This can
be deduced from the ``process/pending review`` label. Now all you have to do
is wait, or let the other developers know on Gitter that you have published
your changes.

Now there's two possibilities:

- your ``Pull Request`` gets accepted, and your commits will get merged into
  the master branch
- your ``Pull Request`` doesn't get accepted, and therefore you will
  need to to modify it as per the review comments

.. note::

    Wait until the reviewer has already reviewed your whole Pull Request
    and has labeled it ``process/wip``. Else, if you push again and his
    comments disappear, it can be considered rude.

.. note::

    You might be wondering what those CI things on your ``Pull Request`` are.
    For more detailed info about them, see
    :doc:`this page <../Help/FAQ>`.

It's highly unlikely that your ``Pull Request`` will be accepted on the first
attempt - but don't worry, that's just how it works. It helps us maintain
coala **clean** and **stable**.

.. seealso::

    `Review Process <http://coala.readthedocs.org/en/latest/Getting_Involved/Review.html>`_.

Now, if you need to modify your code, you can simply edit it again, add it and
commit it using

::

    $ git commit -a --amend

This will edit your last commit message. If your commit message was considered
fine by our reviewers, you can simply send it again like this. If not, edit it
and send it. You have successfully edited your last commit!

.. note::

    Don't forget! After editing your commit, you will have to push it again.
    This can be done using:

::

    $ git push --force myfork

**Congratulations!** Your PR just got accepted! You're awesome.
Now you should go for
`a low issue <tinyurl.com/coala-low>`__,
they are really rewarding!

.. note::

    If you need help picking up an issue, you can always ask us and we'll help
    you!
