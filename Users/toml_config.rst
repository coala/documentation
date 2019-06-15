Writing a coala Configuration File in TOML
======================================================

This document describes how to write configuration files for
coala in TOML format.

Naming, Scope and Location
--------------------------

You can use up to three coafiles to configure your project.

1. A project-wide coafile.
2. A user-wide coafile.
3. A system-wide coafile.

Project-Wide coafile
~~~~~~~~~~~~~~~~~~~~

It is a convention that the project-wide configuration file is named
``.coafile.toml`` and lies in the project root directory.
If you follow this convention, simply executing ``coala -T`` from the
project root will execute the configuration specified in that file.

Settings given in the project-wide configuration file override all settings
given by other files and can only be overridden by settings given via the
command line interface.

User-Wide and System-Wide coafile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can place a ``.coarc.toml`` file in your home directory to set certain
user wide settings. Those settings will automatically be taken for all
projects executed with that user.

All settings specified here override only settings given by the system
wide configuration file which has the lowest priority. The
``system_coafile.toml`` must lie in the coala installation directory
and is valid for everyone using this coala installation.

It can be used to define the type of files you usually don't want to lint,
like minified files (e.g. ``*.min.js``) and backup files (e.g. ``*.orig``)::

    ignore = [ '**.min.js', '**.orig' ]

Basic TOML concepts
---------------------------------
This part describes the basic TOML concepts required to write coala
configuration files

- TOML is case sensitive. So remember to not have duplicate sections/tables
  or duplicate keys in same section.
- key-value pairs are building blocks of a TOML document. Use key-value
  pairs to specify rules for coala bears.
- A table is a collection of key-value pairs. Use a table for specifying
  a coala section.

::

    [cli]
    bears = 'SpaceConsistencyBear'
    files = 'src/*.c'
    use_spaces = true

    [invalidlinks]
    enabled = false
    files = [ '**/*.rst', 'README.rst']
    ignore = 'venv/**'
    bears = 'InvalidLinkBear'

Here tables ``cli`` and ``invalidlinks`` are coala sections.
The contents of the tables like ``bears``, ``files`` are rules
that govern a section. In coala you will be using TOML strings,
booleans, integers and arrays as values.

Section Inheritance
----------------------------
coala supports section inheritance. You can define section inheritance
explicitly by naming a section in the format ``["basesection.newsection"]``.
Extra values can be appended to an inherited setting using the ``appends`` key.

.. note::

    In ``["basesection.newsection"]``, the quotes insides the square braces are
    necessary for specifying section inheritance in TOML.


Consider the following coafile::

  [all]
  enabled = true
  overridable = 2
  ignore = 'vendor1/'

  ["all.section1"]
  overridable = 3
  appends = 'ignore'
  ignore = 'vendor2/'
  other = 'some_value'

  ["all.section2"]
  overridable = 4
  ignore = 'vendor3/'
  appends = 'ignore'
  other = 'some_other_value'


In the inherited sections above, ``appends`` key specifies that the value of
``ignore`` in the derived sections must be appended with the value of
``ignore`` key in the base section. This is the same file without section
inheritance::

  [all]
  enabled = true
  overridable = 2
  ignore = 'vendor1/'

  [section1]
  enabled = true
  overridable = 3
  ignore = ['vendor1/', 'vendor2/']
  other = 'some_value'

  [section2]
  enabled = true
  overridable = 4
  ignore = ['vendor1/', 'vendor3/']
  other = 'some_other_value'


Defining Aspects and Tastes
---------------------------

Aspects is an alternative way to configure coala. In this mode, we don't need
to explicitly state list of bears, coala will choose it automatically based on
requested aspects in configuration file. To run coala in this mode, we need to
define `aspects`, `files`, `languages`, and optionally aspect tastes setting.
See the following example::

  [all]
  files = '**'
  aspects = ['aspectname1', 'AspectName2'] # case-insensitive
  # defining an aspect's taste
  aspectname1.aspect_taste = 80
  # we can define subaspect taste through its parent
  aspectname1.subaspect_taste = ['word1', 'word2', 'word3']

  ['all.python']
  files = '**.py'
  language = 'Python'
  # appending additional aspect
  appends = 'all'
  aspects = 'aspectname3'
  # excluding certain subaspect
  excludes = 'AspectName2Subaspect'

