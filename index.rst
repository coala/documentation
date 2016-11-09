.. coala documentation master file, created by
   sphinx-quickstart on Wed Feb  3 16:49:01 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. meta::
   :description: coala provides a common command-line interface for linting and
                 fixing all your code, regardless of the programming languages
                 you use.
   :keywords:    coala, code analysis, static code analysis, linter,
                 language agnostic, python3, linux, unix, windows, bears,
                 coala-bears

Welcome to the coala documentation!
===================================

.. toctree::
   :caption: Home
   :hidden:

   Welcome <self>

.. toctree::
   :caption: For Users
   :hidden:

   Installing coala <Users/Install>
   Getting Started with coala <Users/Tutorial>
   Writing a coala Configuration File (coafile and coarc) <Users/coafile>
   Using Glob Patterns <Users/Glob_Patterns>
   Exit Codes <Users/Exit_Codes>
   Adding coala as a Git Hook <Users/coala_as_Git_Hook>
   Shell Autocompletion <Users/Shell_Autocompletion>
   coala as a Docker Image <Users/Docker_Image>

.. toctree::
   :caption: For Developers
   :hidden:

   Newcomers' Guide <Developers/Newcomers_Guide>
   Bear Installation Tool <Developers/Bear_Installation_Tool>
   Writing Good Commit Messages <Developers/Writing_Good_Commits>
   Codestyle <Developers/Codestyle>
   Git Basics <Developers/Git_Basics>
   Review <Developers/Review>
   Development Setup <Developers/Development_Setup>
   Writing Bears <Developers/Writing_Bears>
   Writing Linter Bears <Developers/Writing_Linter_Bears>
   Linter Bears - Advanced <Users/Tutorials/Linter_Bears_Advanced>
   External Bears <Developers/External_Bears>
   Testing Bears <Developers/Testing_Bears>
   Writing Tests <Developers/Writing_Tests>
   Writing Documentation <Developers/Writing_Documentation>
   Executing Tests <Developers/Executing_Tests>

.. toctree::
   :caption: Help
   :hidden:

   How To Get In Touch With Us <Help/Getting_In_Touch>
   Frequently Asked Questions <Help/FAQ>
   MAC Hints <Help/MAC_Hints>

You might also want to look at `our website <http://coala.io/>`_.

.. image:: https://cloud.githubusercontent.com/assets/7521600/15992701/ef245fd4-30ef-11e6-992d-275c5ca7c3a0.jpg

coala: Language Independent Code Analysis
-----------------------------------------

**coala provides a unified command-line interface for linting and fixing all
your code, regardless of the programming languages you use.**

With coala, users can create
:doc:`rules and standards <Users/coafile>` to be followed in the source
code. coala has an **user-friendly interface** that is completely customizable.
It can be used in any environment and is completely modular.

coala has a set of official bears (plugins) for several languages, including
popular languages such as **C/C++**, **Python**, **JavaScript**, **CSS**,
**Java** and many more, in addition to some generic language independent
algorithms. To learn more about the different languages supported and the
bears themselves,
`click here. <https://github.com/coala/bear-docs/blob/master/README.rst>`__

.. note::

  To see what coala can do for you and your language, take a look at
  `our capabilities listing <https://github.com/coala/bear-docs/blob/master/README.rst>`__.

If you are here to use coala for your own projects, take a look at our
:doc:`installation guide<Users/Install>`.

If you want to start contributing to coala, you can follow our
:doc:`tutorial for newcomers<Developers/Newcomers_Guide>` which aims to get
everyone to fix an issue by themselves.

.. note::

  To contact us, always feel free to check our
  :doc:`Getting In Touch<Help/Getting_In_Touch>` page.

What do I get?
--------------

As a User
~~~~~~~~~

coala allows you to simply check your code against certain quality
requirements. The checking routines are named **Bears** in coala. You
can easily define a simple project file to check your project with all
bears either shipped with coala or ones you found in the internet and
trust.

As a Developer
~~~~~~~~~~~~~~

If you are not satisfied with the functionality given by the bears we
provide, you can easily write your own bears. coala is written with easiness
of extension in mind. That means: no big boilerplate, just write one
small object with one routine, add the parameters you like and see how
coala automates the organization of settings, user interaction and
execution parallelization. You shouldn't need to care about anything
else than just writing your algorithm!

.. seealso::

  Check out :doc:`Writing Bears <Developers/Writing_Bears>` for more
  information on this.

To programmatically access coala's functionality, use ``coala-json`` or
``coala-format`` if you want to use a custom format string. Both of those
binaries, among with ``coala-ci``, are noninteractive and thus suitable for
continuous integration.

.. seealso::

  Check :doc:`External APIs <Users/External_APIs>` for more information.

Status and Stability of the Project
-----------------------------------

We are currently working hard to make this project reality. coala is currently
usable, in beta stage and already provides more features than most
language dependent alternatives. Every single commit is fully reviewed and
checked with various automated methods including our testsuite covering all
branches. Our master branch is continuously prereleased to our users so you can
rely on the upcoming release being rock stable.

If you want to see how the development progresses, check out
`coala <https://github.com/coala/coala>`__ and
`coala-bears <https://github.com/coala/coala-bears>`__.
