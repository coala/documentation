Bear Installation Tool
======================

coala features a Bear Installation Tool that helps installing bears one by one
or all of them. This tool is helpful as it also manages to install the bears'
external dependencies.

Installation
------------

To install the tool, simply run:

::

    $ pip3 install coala-install

Usage
-----
To use the tool, run

::

    $ coala-install

and a question will pop-up. To install all the bears, simple type ``All``.
If you want just a few bears, type ``Some``. Then, a list with all the
bears, collected from PyPI, will pop up. You will now have to choose the bears
you want to install, separated by commas, and along with the dependencies,
the bears will install. To quit, simply type anything else.

The tool features syntax highlighting, which highlights the options that are
in the given lists, and also autocompletion.

Developer Insight
-----------------

The tool gathers all the bear packages from PyPI using the one thing only they
have in common: the coala website in the description. Then it generates a list,
pops it up and installs all the packages.
