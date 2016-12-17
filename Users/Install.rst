Installing coala Natively
=========================

.. note::

    If you have a working docker and you do not want to work with python,
    go to the bottom on the docker setup.

This page will run you through the installation of coala without docker. coala
currently supports Linux and Windows, and is known to work on OS X (meaning we
do not have continuous integration for it but it works).

Installing Python and Pip
--------------------------

In order to use coala, you need Python installed. In order to do so, you should
install Python >= 3.4 from `here <https://www.python.org/downloads/>`_.

The easiest way to install coala is using pip (Pip Installs Packages).
If you don't already have pip, you can install it like described in the
`pip installation guide <https://pip.pypa.io/en/stable/installing.html>`_.

.. note::

  Pip is shipped with recent Python versions by default.

To check whether you have pip installed, type the following command which will
also show you more information about your current pip version:
::

    $ pip show pip

Installing coala
----------------

There are three ways of installing coala. By using a virtualenv, by installing
it system-wide or directly from source.

After successfully installing coala, you will need to install all the
dependencies the bears have.

System Wide Installation
~~~~~~~~~~~~~~~~~~~~~~~~

The simplest way to install coala is to do it system-wide, but this is
generally discouraged in favor of using a virtualenv.

To install the latest most stable version of coala and supported bears
system-wide, use:

::

    $ pip3 install coala-bears

.. note::

    For this and all future steps, some steps require root access
    (also known as administrative privileges in Windows).

    **Unix based** (OS X, Linux) - This can be achieved by using ``sudo``
    in front of the command, as in: ``sudo command_name`` instead of
    ``command_name``

    **Windows** - The easiest way on Windows is to start a
    command prompt as an administrator and start ``setup.py``.

To install the nightly build from our master branch, you can do:

::

    $ pip3 install coala-bears --pre

To install coala only (without any bears), you can do:

::

    $ pip3 install coala

Installing inside a virtualenv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Virtualenv is probably what you want to use during development.
You can read more about
it at the `virtualenv documentation <http://virtualenv.readthedocs.org>`_.

First, we need to install virtualenv to the system. You may already have this
installed as ``virtualenv`` or ``pyvenv``. If you do not, this can be done
with ``pip3`` easily:

::

    $ pip3 install virtualenv

Once you have virtualenv installed, just fire up a shell and create
your own environment. I usually create a project folder and a ``venv``
folder:

::

    $ virtualenv venv

Now, whenever you want to work on the project, you only have to activate
the corresponding environment.

    On **Unix based** systems (OS X and Linux), this can be done with:

    ::

        $ source venv/bin/activate

    And on **Windows** this is done with:

    ::

        $ venv\scripts\activate

Finally, you should install coala and the supported bears inside the activated
virtualenv with:

::

    (venv)$ pip3 install coala-bears

Using coala With Docker
=======================

Use this installation method if you *just simply want to use coala*.

The recommended way to use coala is using docker: coala has a lot of
dependencies because it has so much code analysis for so many languages. If you
use our docker image, you can run it like any other tool but you do not need to
care about those! The general command to run coala is:

::

    $ docker run -ti -v $(pwd):/app --workdir=/app coala/base coala --version

.. note::

    This will automatically download the docker image with all the coala
    dependencies for you. The image may take up a bit over 2GB of space on your
    disk. Check out the native installation if this is not for you.

Windows
-------

If you use windows, you can install docker easiest
[here](https://www.docker.com/products/docker-toolbox).

Installing coala from source
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you would like to develop coala, you should check out our
`Newcomer Tutorial <http://coala.io/newcomer>`_ and
:doc:`get in touch with us <../Help/Getting_In_Touch>`.

If you only desire to use the latest development version of coala, then you
can run

::

    (venv)$ git clone https://github.com/coala/coala
    (venv)$ cd coala
    (venv)$ pip3 install .
    (venv)$ cd -
    (venv)$ git clone https://github.com/coala/coala-bears
    (venv)$ cd coala-bears
    (venv)$ pip3 install .

which will always install the most recent code from our master branch.

Alternate location installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you want to install coala to an alternate location, you can e.g. call
``python3 setup.py install --prefix=/your/prefix/location``. Other installation
options are documented in the
`Python docs <https://docs.python.org/3.4/install/#alternate-installation>`_.

.. note::

    If you are using a proxy, follow these steps:

    -  Set up your system-wide proxy.
    -  Use ``sudo -E pip3 install coala`` (the ``-E`` flag takes the
       existing environment variables into the ``sudo`` environment).

    You could also set your pip.conf file to use a proxy. To find out more,
    read `Using pip behind a proxy on StackOverflow
    <http://stackoverflow.com/questions/14149422/using-pip-behind-a-proxy>`_
    for further clarification.

Optional Dependencies
---------------------

Those dependencies are not mandatory. You may install all of the
dependencies if you want to install all the bears. The bear
application also asks for the packages needed in case it does not
have it.

The requirements files ( Gemfile, requirements.txt, etc.) are in
the coala-bears repository and you should not get them from 
source, but you should git clone the repository if you want to
execute those commands.

This section lists dependencies of coala that are not automatically
installed. On Windows, you can get many with ``nuget``
(https://www.nuget.org/). On Mac, Homebrew will help you installing
dependencies (http://brew.sh/). These dependencies require you to have
`the repository <https://github.com/coala/coala-bears>`__
cloned locally.

JS Dependencies
~~~~~~~~~~~~~~~

coala features a lot of bears that use linters written in JavaScript. In
order for them to be usable, you need to install them via ``npm``
(http://nodejs.org/), while in the project directory:

::

    $ npm install -g

If a bear still doesn't work for you, please make sure that you have a
recent version of ``npm`` installed. Many linux distributions ship a
very old one.

Ruby Dependencies
~~~~~~~~~~~~~~~~~

There are also a few bears which rely on Ruby Gems. In order to install them,
you will need ``Gem`` (https://rubygems.org/pages/download/) installed
and ``bundler``.

To grab ``bundler``, use:

::

    $ gem install bundler

Then, simply run:

::

    $ bundle install
    $ git add Gemfile Gemfile.lock

Binary Dependencies
~~~~~~~~~~~~~~~~~~~

Some bears need some binary dependencies. Some of those include:

-  PHPLintBear: Install ``php``
-  GNUIndentBear: Install ``indent`` (be sure to use GNU Indent, Mac ships
   a non-GNU version that lacks some functionality.)
-  CSharpLintBear: Install ``mono-mcs``

For further help with installing bears with binary dependencies, don't hesitate
to
:doc:`get in touch with us <../Help/Getting_In_Touch>`.

Clang
~~~~~

coala features some bears that make use of Clang. In order for them to
work, you need to install ``libclang``:

-  Ubuntu: ``apt-get install libclang1``
-  Fedora: ``dnf install clang-libs`` (Use ``yum`` instead of ``dnf`` on
   Fedora 21 or lower.)
-  ArchLinux: ``pacman -Sy clang``
-  Windows: ``nuget install ClangSharp``
-  OS X: ``brew install llvm --with-clang``

If these do not help you, search for a package that contains
``libclang.so``.

On Windows, you need to execute this command to add the libclang path to
the *PATH* variable permanently (you need to be an administrator):

``setx PATH "%PATH%;%cd%\ClangSharp.XXX\content\x86" \M``

For x86 python or for x64 python:

``setx PATH "%PATH%;%cd%\ClangSharp.XXX\content\x64" \M``

Replace "XXX" with the ClangSharp version you received from nuget.

Installation Errors
-------------------

In case you are getting
``ValueError:('Expected version spec in', 'appdirs ~=1.4.0', 'at',
' ~=1.4.0')``, then don't panic. It happens when you are using an outdated
version of pip that doesn't support our version specifiers yet.


    Ideally, you have to create a virtual environment with a newer pip:

    ::

        $ pip3 install virtualenv
        $ virtualenv -p python3 ~/venv/coala
        $ . ~/venv/coala/bin/activate
        $ pip install -U pip
        $ pip install coala-bears

You have to activate this virtualenv on every terminal session you want to use
coala though (tip: add it to bashrc!).

Generating Documentation
~~~~~~~~~~~~~~~~~~~~~~~~

coala documentation is
`in a separate repository <https://github.com/coala/documentation>`__.
First you need to install the requirements:

::

    $ pip3 install -r docs-requirements.txt

To generate the documentation coala uses `sphinx`. Documentation can be
generated by running the following command while in root directory of the
repository:

::

    $ make html

You can then open ``_build\html\index.html`` in your favourite
browser.

See `Writing Documentation <http://api.coala.io/en/latest/Developers/Writing_Documentation.html>`_
for more information.
