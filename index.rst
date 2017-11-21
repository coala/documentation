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
   MAC Hints <Help/MAC_Hints>
   How To Get In Touch With Us <Help/Getting_In_Touch>
   Frequently Asked Questions <Help/FAQ>

.. toctree::
   :caption: For Developers
   :hidden:

   coala API Documentation <https://api.coala.io>


You might also want to look at `our website <http://coala.io/>`_.

.. image:: _static/images/coala-header.png
   :scale: 50
   :align: center

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
`click here. <https://coala.io/#/languages>`__

.. note::

  To see what coala can do for you and your language, take a look at
  `our capabilities listing <https://coala.io/#/languages>`__.

If you are here to use coala for your own projects, take a look at our
:doc:`installation guide<Users/Install>`.

If you want to start contributing to coala, you can follow our
`tutorial for newcomers`_ which aims to get
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

  Check out `Writing Bears`_ for more
  information on this.

To programmatically access coala's functionality, use the ``--json`` option.
Use the ``--format`` option if you want to use a custom format string. Both of
these arguments along with ``--ci`` argument run coala in non-interactive mode
which is suitable for continuous integration.

Hint
~~~~

``--json`` makes the coala output easy to read and understand. It consists of
a collection of name/value pairs usually represented by objects and an ordered
list of values stored in arrays. You can read more about this format `here
<http://www.json.org>`__.

``--format`` has a linear, one line return. Its output can be easily parsed
as it is fully customizable. This option will not show all the tested areas
but those with issues. In case of no errors, ``--format`` will have no output.

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


.. _tutorial for newcomers: https://coala.io/newcomers
.. _Writing Bears: https://coala.io/writingbears
