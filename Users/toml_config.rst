Writing a coala Configuration File in TOML
======================================================

This document describes how to write configuration files for
coala in TOML format.

Naming, Scope and Location
--------------------------

You can use up to three configuration files to configure your project.
Two of these configuration files ``.coarc.toml`` and ``system_coafile.toml``
can be the same for any number of projects but ``.coafile.toml`` can be
different for different projects.

1. A project-wide configuration file.
2. A user-wide configuration file.
3. A system-wide configuration file.

Project-Wide configuration file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

It is a convention that the project-wide configuration file is named
``.coafile.toml`` and lies in the project root directory.
If you follow this convention, simply executing ``coala -T`` from the
project root will execute the configuration specified in that file.

Settings given in the project-wide configuration file override all settings
given by other files and can only be overridden by settings given via the
command line interface.

User-Wide and System-Wide configuration file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

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
---------------------
This part describes the basic TOML concepts required to write coala
configuration files in TOML

- TOML is case sensitive. So remember to not have duplicate sections/tables
  or duplicate keys in same section.
- key-value pairs are building blocks of a TOML document. Use key-value
  pairs to specify rules for coala bears.
- A table is a collection of key-value pairs. Use a table for specifying
  a coala section.

A list of settings required to write configuration can be found at
`Settings
<http://api.coala.io/en/latest/Developers/coala_settings.html>`_

This is an example of a coala configuration file written in TOML

.. code::

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
that govern a section. To write coala configuration file you will
be using TOML strings, booleans, integers and arrays as values.

Section Inheritance
---------------------
coala supports section inheritance. You can define section inheritance
by using the key ``inherits``.
Extra values can be appended to an inherited setting using the ``appends`` key.

Consider the following configuration file in TOML

.. code::

  [all]
  enabled = true
  overridable = 2
  ignore = 'vendor1/'

  [section1]
  overridable = 3
  inherits = 'all'
  appends = 'ignore'
  ignore = 'vendor2/'
  other = 'some_value'

  [section2]
  overridable = 4
  inherits = 'all'
  ignore = 'vendor3/'
  appends = 'ignore'
  other = 'some_other_value'


In the inherited sections above, ``appends`` key specifies that the value of
``ignore`` in the derived sections must be appended with the value of
``ignore`` key in the base section.

This is the same file without section inheritance

.. code::

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


Consider another example

Config file in TOML

.. code::

 [all]
 a = 1
 b = 2

 [java]
 c = 3
 d = 4

 [python]
 p = 5
 q = 6
 inherits = [ 'all', 'java']

You can use this syntax to specify multiple inheritance
The same in coafile format appears as

.. code::

 [all]
 a = 1
 b = 2

 [java]
 c = 3
 d = 4

 [all.python]
 a = 1
 b = 2
 p = 5
 q = 6

 [java.python]
 c = 3
 d = 4
 p = 5
 q = 6

.. note::

   - If you want to append multiple settings then use ``appends`` as a list
     ::

        appends = [ 'a', 'b']
   - If you want to inherit multiple sections use ``inherits`` as a list
     ::

        inherits = [ 'section1', 'section2']
   - You can only inherit sections
   - You can only append settings
   - If  a setting is redefined in the inherited section then it will
     overwritten if appends is not used.

Defining Aspects and Tastes
----------------------------

Aspects is an alternative way to configure coala. In this mode, we don't need
to explicitly state list of bears, coala will choose it automatically based on
requested aspects in configuration file. To run coala in this mode, we need to
define `aspects`, `files`, `languages`, and optionally aspect tastes setting.
See the following example

.. code::

  [all]
  files = '**'
  aspects = ['aspectname1', 'AspectName2'] # case-insensitive
  # defining an aspect's taste
  aspectname1.aspect_taste = 80
  # we can define subaspect taste through its parent
  aspectname1.subaspect_taste = ['word1', 'word2', 'word3']

  [python]
  files = '**.py'
  language = 'Python'
  inherits = 'all'
  # appending additional aspect
  appends = 'all'
  aspects = 'aspectname3'
  # excluding certain subaspect
  excludes = 'AspectName2Subaspect'

For coafile users who want to write configuration in TOML

- If you are using aspects  ``a:b = 'c'``  in a section named `example`
  then replace ``a:b = 'c'`` with ``a.b = 'c'`` or

  .. code::

   [example.a]
   b = 'c'

For existing coala users who want to use TOML
---------------------------------------------

In this section we will see how to convert a complex coafile into
a configuration file in TOML

.. code::

 [all]
 files = *.py, coantlib/**/*.py, tests/**/*.py, coantbears/**/*.py, .ci/*.py
 max_line_length = 80
 use_spaces = True

 [all.python]
 # Patches may conflict with autopep8 so putting them in own section so they
 # will be executed sequentially; also we need the LineLengthBear to double
 # check the line length because PEP8Bear sometimes isn't able to correct the
 # linelength.
 bears = SpaceConsistencyBear
 language = Python
 preferred_quotation = '
 default_actions = **: ApplyPatchAction

 [all.flakes]
 # Do not set default_action to ApplyPatchAction as it may lead to some
 # required imports being removed that might result in coala behaving weirdly.
 default_actions = *: ShowPatchAction
 bears += PyUnusedCodeBear
 language = Python
 remove_all_unused_imports = true

To convert a coafile to configuration file in TOML

- Enclose all string values in quotes
- Use array notation to depict list of strings
- Replace ``[parent_section.inherited_section]`` with ``[inherited.section]``
  and add ``inherits = parent_section`` as a key-value pair
- Use ``true`` or ``false`` to specify booleans
- Replace ``a += b`` with

.. code::

   a = 'b'
   appends = 'a'


Using the above rules we get a configuration file in TOML

.. code::

 [all]
 files = ['*.py', 'coantlib/**/*.py', 'tests/**/*.py', 'coantbears/**/*.py',
         '.ci/*.py']
 max_line_length = 80
 use_spaces = true

 [python]
 # Patches may conflict with autopep8 so putting them in own section so they
 # will be executed sequentially; also we need the LineLengthBear to double
 # check the line length because PEP8Bear sometimes isn't able to correct the
 # linelength.
 inherits = 'all'
 bears = 'SpaceConsistencyBear'
 language = 'Python'
 preferred_quotation = '
 default_actions = '**: ApplyPatchAction'

 [flakes]
 # Do not set default_action to ApplyPatchAction as it may lead to some
 # required imports being removed that might result in coala behaving weirdly.
 inherits = 'all'
 default_actions = '*: ShowPatchAction'
 bears = 'PyUnusedCodeBear'
 appends = 'bears'
 language = 'Python'
 remove_all_unused_imports = true
