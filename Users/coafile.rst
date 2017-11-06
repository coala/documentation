Writing a coala Configuration File (coafile and coarc)
======================================================

This document gives a short introduction to the specification of a
coala configuration file. It is meant to be rather factual. If you wish
to learn by example, please take a look at :doc:`Tutorial`. It also
teaches how to change settings inside a coala file to suit your taste.

Naming, Scope and Location
--------------------------

You can use up to three coafiles to configure your project.

1. A project-wide coafile.
2. A user-wide coafile.
3. A system-wide coafile.

Project-Wide coafile
~~~~~~~~~~~~~~~~~~~~

It is a convention that the project-wide coafile is named ``.coafile``
and lies in the project root directory. If you follow this convention,
simply executing ``coala`` from the project root will execute the
configuration specified in that file.

Settings given in the project-wide coafile override all settings given
by other files and can only be overridden by settings given via the
command line interface.

User-Wide and System-Wide coafile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can place a ``.coarc`` file in your home directory to set certain
user wide settings. Those settings will automatically be taken for all
projects executed with that user.

All settings specified here override only settings given by the system
wide coafile which has the lowest priority. The ``default_coafile`` must
lie in the coala installation directory and is valid for everyone using
this coala installation.

Explicit Setting Inheritance
----------------------------

Every coafile contains one or more sections. Section names are case
insensitive. The old(pre 0.11.x) implicit section inheritance syntax
has been deprecated and has been scheduled for removal in coala version 0.12.0.
Instead, define section inheritance explicitly by naming a section in the
format ``[basesection.newsection]``. Extra values can be appended to an
inherited setting using the ``+=`` operator.

Consider the following coafile::

  [all]
  enabled = True
  overridable = 2
  ignore = vendor1/

  [all.section1]
  overridable = 3
  ignore += vendor2/
  other = some_value

  [all.section2]
  overridable = 4
  ignore += vendor3/
  other = some_other_value

This is the same file without section inheritance::

  [all]
  enabled = True
  overridable = 2
  ignore = vendor1/

  [section1]
  enabled = True
  overridable = 3
  ignore = vendor1/, vendor2/
  other = some_value

  [section2]
  enabled = True
  overridable = 4
  ignore = vendor1/, vendor3/
  other = some_other_value

All settings must be part of a section, so don't do this for implicit
inheritance (this is also deprecated behavior). Implicit inheritance
was leading to a section automatically getting inherited to all other
sections without semantically making sense.

  # bad!
  setting1 = 1

  [section1]
  # setting1 is inherited
  setting2 = 2

Instead, make the inheritance explicit::

  # better!
  [all]
  setting1 = 1

  [all.section1]
  # setting1 is inherited
  setting2 = 2

Defining Aspects and Tastes
---------------------------

Aspects is an alternative way to configure coala. In this mode, we don't need
to explicitly state list of bears, coala will choose it automatically based on
requested aspects in coafile. To run coala in this mode, we need to define
`aspects`, `files`, `languages`, and optionally aspect tastes setting. See
the following example::

  [all]
  files = **
  aspects = aspectname1, AspectName2 # case-insensitive
  # defining an aspect's taste
  aspectname1:aspect_taste = 80
  # we can define subaspect taste through its parent
  aspectname1:subaspect_taste = word1, word2, word3

  [all.python]
  files = **.py
  language = Python
  # appending additional aspect
  aspects += aspectname3
  # excluding certain subaspect
  excludes = AspectName2Subaspect

Comments, Escaping and Multiline Values and Keys
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Comments are simply done with a preceding ``#``. If you want to use a
``#`` within a value, you can simply escape it:

::

    a_key = a\#value # And a comment at the end!

Any line not containing an unescaped ``=`` is simply appended to the
value of the last key:

::

    a_key = a
    value
    # this is not part of the value, as this is a comment line
    that /= is
    very long!

``a_key`` is set to ``a value that = is very long!``

Similarly, you can also set a value to multiple keys:
``key_1, key_2 = value`` is equivalent to ``key_1 = value`` and
``key_2 = value`` in separate lines.

As the backslash is the escape character it is recommended to use
forward slashes as path separator even on Windows (to keep relative
paths platform independent), use double-backslashes if you really mean a
backslash in all places.

You can now proceed to an example with :doc:`Tutorial`.
