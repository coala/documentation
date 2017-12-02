Frequently Asked Questions
==========================

This is a list of frequently asked questions, aiming to answer any possible
questions by newcomers or even contributors.

.. contents:: Table of Contents

What does coala do (for me)?
----------------------------

coala is like a spell and grammar checker for source code. It offers one
command and one configuration to lint all languages in your project.

In short coala does two things:

- Makes it easy to use existing static code analyzers such as clang,
  pylint(and many others) by unifying and simplifying the configs
- Makes it easy to write new routines by offering the interface part and
  everything but the actual analyzer routine. Write just the parameters
  your custom analysis needs and the analysis part, we'll take care of the rest

Can I Use coala in my Continuous Integration?
---------------------------------------------

Yes! There's an argument *--ci* that runs the coala binary in non-interactive
mode, which shows results cleanly in the log and returns error codes
if something goes wrong. List of the exit codes and their meanings:
`Exit Codes <https://docs.coala.io/en/latest/Users/Exit_Codes.html>`__.

Why did you choose the name?
----------------------------

coala stands for "COde AnaLysis Application", works well with animals and thus
is well visualizable, it's easy to memorize.

Is there corporate backing behind coala? What are your intentions?
------------------------------------------------------------------

coala was founded for fun. coala was, is and will always be free software and
is developed mostly by students and there's no corporate interest and no CLA.
If you want to back us, contact us on our
`gitter channel <https://coala.io/chat>`__.

What sort of analysis does coala do? What languages are supported?
------------------------------------------------------------------

A list of all analysis routines and supported languages is
`fully browsable <https://coala.io/#/languages>`__.

For a top level view on what languages support what kind of analysis roughly,
consult `this link <https://docs.google.com/spreadsheets/d/1bm63TQHndmGf3HQ33fp9UEmGKNYI7dTkjMyFIof2PqA/edit?usp=sharing>`__.

There are also generic bears, which can be applied language independently on
your code. Their capabilities and information can be seen
`here <https://coala.io/#/languages>`__.

How do I get started with coala?
--------------------------------

If you're looking to get started using coala, we have a
:doc:`full tutorial <../Users/Tutorial>`
that will teach you everything you need to know to use coala.

If you're willing to contribute and become a part of our coalaian community,
we have written a `newcomers guide <http://coala.io/newcomer>`_ that will help
you fix an issue on your own, just by following and understanding the
indications.
It is meant for newcomers, and it does not require you to have any precedent
knowledge regarding coala.

How do I get in touch with the coala team?
------------------------------------------

We are very active on our
`gitter channel <https://coala.io/chat>`__
and will try to respond to any question in a matter of minutes.
However, for a full list of how to get in touch with us, consult
:doc:`this link <Getting_In_Touch>`.

Installation is Failing! Help!
------------------------------

Don't panic!

Scroll down the error log, you will probably see something like `ValueError:
('Expected version spec in', 'appdirs ~=1.4.0', 'at', ' ~=1.4.0')` there.
If not, `ask us! <http://coala.io/chat>`__

If so, you're probably on a Debian with an outdated pip that doesn't support
our version specifiers yet. You have to create a virtual environment with
a newer pip:

.. code-block:: bash

  pip3 install virtualenv
  virtualenv -p python3 ~/venvs/coala
  . ~/venvs/coala/bin/activate
  pip install -U pip
  pip install coala-bears


should do the job. You have to activate this virtualenv on every terminal
session you want to use coala though (tip: add it to bashrc!)

What are those things failing/passing on my Pull Request?
---------------------------------------------------------

We use a few checks to make sure your Pull Request is ready to be merged into
our master branch. Right now we use 7 of those checks:

- **review/gitmate/commit** Checks this particular commit has any new gitmate
  issues.

- **review/gitmate/pr** Checks whether your code respects our styling (PEP8),
  doesn't contain unneeded newlines, trailing whitespace, etc. Basically it is
  like running coala over your code, so to fix this, simply run ``$ coala``
  before pushing! In case you have multiple commits, and the issue is in one
  of them, the status will still be failed, so be careful to run ``$ coala``
  before making each commit.

- **review/gitmate/manual** This one is the only one that is manual, this can
  be given by any coala member and shows that the commit has been reviewed and
  has no problems, so it is ready to be merged. It can be done by commenting
  ``ack commit_sha``. For more information about the whole process, we have
  it all documented
  `here <http://api.coala.io/en/latest/Developers/Review.html>`_.

- **codecov/project** This one checks whether all your code is being tested. We
  cannot merge anything that may not work or may broke somewhere, so to avoid
  obvious bugs we use this. To fix it, write doctests or unittests for your
  functions / classes.

- **ci/circleCI** This is one of the two containers we use to continuously
  test the code. It basically runs all the tests and checks your code in a
  container, checking that the tests pass on the container. This one is for
  Linux, it runs Ubuntu 12.04.

- **continuous-integration/appveyor/pr** This one does the same as the one
  above, but for Windows, both 32 and 64bits versions.
