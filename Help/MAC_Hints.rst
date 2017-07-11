Coverage Installation Hints for macOS Users:
============================================

venv
----

Here we will be using ``venv``, which is part of python's standard
libary since python 3.3, to create a virtualenv for development.

1. Make sure you have installed Xcode and Homebrew.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2. Install Python 3.
~~~~~~~~~~~~~~~~~~~~

For coala you will need to use Python 3, so you may
simply use homebrew to install Python 3, or you could also
`refer to the pyenv section <#pyenv>`__ to install Python 3 while you can also
maintain other python versions.

::

    $ brew search python  # This should display Python 3
    $ brew install python3
    $ python3 --version   # To check the installed version

3. Create Virtual Environments with venv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    # Create Virtual Env named myenv
    $ python3 -m venv myenv

    # This will create a folder named myenv in the
    # current directory. To activate this environment just type
    $ source myenv/bin/activate

    # You can start Python 3 by typing:
    $ python

4. Virtualenvwrapper with Python 3:
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    # Installation
    $ pip3 install virtualenv
    $ pip3 install virtualenvwrapper

    # Folder to contain Virtual Environments
    $ mkdir ~/.virtualenvs

    # Add the following in ~/.bash_profile
    $ export WORKON_HOME=~/.virtualenvs
    $ source /usr/local/bin/virtualenvwrapper.sh

    # Activate Changes
    $ source ~/.bash_profile

    # Get Python 3 path (python3_pth)
    $ which python3

    # Create a new virtual environment with Python 3
    $ mkvirtualenv --python=python3_path myenv

Finally!
~~~~~~~~

::

    # Install python-coverage3 by
    $ easy_install coverage

pyenv
-----

Here we show how to use pyenv, which is simply a python installer
that allows you to install multiple python versions and switch
through them. After installation, you may also want to set up
a virtual environment using :code:`venv` or :code:`virtualenv`.

1. Install pyenv with homebrew
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

::

    $ brew update
    $ brew install pyenv

2. Installing and using python with pyenv
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To install python you simply have to
do this (you don't have to install all of them) :

::

    $ pyenv install 3.5.0
    $ pyenv install 3.4.3
    $ pyenv install 3.3.6
    $ pyenv install 3.2.6
    $ pyenv install 2.7.10
    $ pyenv versions # lists the versions you have

To use a particular version you simply have to do this :

::

    $ pyenv local 3.5.0

To know more about the available pyenv commands, please
read their `Command Reference
<https://github.com/pyenv/pyenv/blob/master/COMMANDS.md>`__.


Presently, while using pyenv, tests for version-file-read fail,
if interested you can
have a look `here <https://github.com/yyuu/pyenv/issues/623>`__.
