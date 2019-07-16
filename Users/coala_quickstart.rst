Using coala-quickstart to Generate a coala Configuration File
=============================================================

This document aims to make people aware of coala-quickstart by providing a
brief introduction about its features and how to quickly generate
coala configuration files for your projects.

What is coala-quickstart?
-------------------------

coala-quickstart is a CLI tool that helps users to quickly get started with
coala by generating a ``.coafile`` tailored for their project. The ``.coafile``
is generated based on the questions answered by the users about their project.

Features
--------

coala-quickstart offers the following features:

- Out-of-the-box support for projects using various popular languages such as
  C/C++, Python, JavaScript and many more with built-in check routines.
- Automatic detection of languages used in your project.
- Automatic identification of bears that might be relevant for your project and
  detection of bear settings based on the languages used.
- A clean and simple interface with a well defined flow.

Installation
------------

To install the latest stable version run:

::

    $ pip3 install coala-quickstart

To install the latest development version run:

::

    $ git clone https://github.com/coala/coala-quickstart.git
    $ cd coala-quickstart
    $ pip3 install .

Usage
-----

To get started simply run:

::

    $ coala-quickstart

This should prompt you for your project's directory. If you want to use your
current directory, just press the return key.

It will detect the languages used in your project and provide a percentage
distribution of those languages in your project. You will now be presented
with a list of bears that might be relevant to your project to choose from.
Once you choose your bears you are done.

At the end, you should have a file named ``.coafile`` generated at the root of
your project directory. This contains all the settings needed by coala to lint
and fix your code. You can also open the .coafile in your favorite editor and
edit the settings to suit your needs.

Once you have completed these steps just execute coala from your project's
root:

::

    $ coala

coala-quickstart can also generate configuration files in TOML.
To generate a configuration file in TOML use

::

    $ coala-quickstart - T

Once you have completed these steps just execute coala from your project's
root:

::

    $ coala -T
