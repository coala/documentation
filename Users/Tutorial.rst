Getting Started with coala
==========================

Welcome to this little tutorial. It is meant to be a gentle introduction
to the usage of coala.

Prerequisites
-------------

In order to complete this tutorial you will need coala installed.
Installation instructions can be found `here <https://coala.io/install>`_.

.. note::

    Here's a list of our
    `supported languages
    <https://coala.io/#/languages>`__.


Get Some Code
-------------

In order to perform a static code analysis on your code you will need
some code to check. If you do not have your own code you want to check, you
can retrieve our tutorial samples:

::

    git clone https://github.com/coala/coala-tutorial

Please note that the commands given in this tutorial are intended for
use with this sample code and may need minor adjustments.

Let's Start!
------------

There are two options how to let coala know what kind of analysis it
should perform on which code.

Command Line Interface
~~~~~~~~~~~~~~~~~~~~~~

In order to specify the files to analyze, you can use the ``--files``
argument of coala like demonstrated below. For all file paths, you can
specify (recursive) `globs <../Users/Glob_Patterns.html>`__.

Because analysis routines can do many various things we named them
**bears**. A bear can check your code for potential problems, calculate metrics
and even provide corrections for your code.

You can specify the bears that you want coala to run using the ``--bears``
argument:

::

    cd coala-tutorial
    coala --files=src/\*.c --bears=SpaceConsistencyBear --save

.. note::

    You can use comma separated values to specify more than one item in
    arguments! Do not use spaces as that would start a new argument.
    Example: ``SpaceConsistencyBear,PEP8Bear``

coala will now ask you for missing values that are needed to perform the
analysis, which in this case is only the ``use_spaces`` setting. We
recommend setting it to ``True``.

::

    Please enter a value for the setting "use_spaces" (True if spaces
    are to be used instead of tabs.) needed by SpaceConsistencyBear
    for section "cli"

coala will now check the code and, in case you use the tutorial code,
yield one result. SpaceConsistencyBear will detect a trailing whitespace at
the end of the line, after ``#include <stdio.h>`` in the ``main.c`` file. coala
will then ask you to remove the trailing space, by applying the suggested
patch (option 2).

::

    Executing section cli...

    src/main.c
    |   1| #include·<stdio.h>·
    |    | [NORMAL] SpaceConsistencyBear:
    |    | Line contains following spacing inconsistencies:
    |    | - Trailing whitespaces.
    |----|    | /path/coala-tutorial/src/main.c
    |    |++++| /path/coala-tutorial/src/main.c
    |   1|    |-#include <stdio.h>
    |    |   1|+#include <stdio.h>
    |   2|   2|
    |   3|   3| int main(void) {
    |   4|   4|     printf("Welcome to coala. Keep following the
                    tutorial, you are doing a great job so far!\n");
    |    | *0: Do nothing
    |    |  1: Open file(s)
    |    |  2: Apply patch
    |    |  3: Print more info
    |    |  4: Add ignore comment
    |    | Enter number (Ctrl-D to exit): 2

If the patch was applied succesfully, you should see something like this:

::

    |    | Patch applied successfully.
    |    | *0: Do nothing
    |    |  1: Open file(s)
    |    |  2: Print more info
    |    |  3: Add ignore comment
    |    | Enter number (Ctrl-D to exit):

Exit by pressing Ctrl-D.

You can also run coala in non interactive mode (given that all the settings
required by the bears you are using are provided in the ``.coafile``)

::

    coala  --non-interactive

In this case there won't be any interaction, the patch will be shown directly.

Feel free to experiment a bit. You've successfully analysed some code!
But don't stop reading - you don't have to enter all those values again!
We have given coala the ``--save`` argument, which means that it will
automatically generate a ``.coafile`` into the current directory. Read on!

Configuration Files - coafiles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

coala supports a very simple configuration file. If you've executed the
instructions from the CLI section above, coala will already have such a
file readily prepared for you. Before starting work with coafiles read the description of it. There are three types of coafiles:

1. A project-wide coafile.
2. A user-wide coafile.
3. A system-wide coafile

Project- wide cofile
^^^^^^^^^^^^^^^^^^^^
It is a convention that the project-wide coafile is named ``.coafile``
and lies in the project root directory. If you follow this convention,
simply executing ``coala`` from the project root will execute the
configuration specified in that file.

Settings given in the project-wide coafile override all settings given
by other files and can only be overridden by settings given via the
command line interface.

User-Wide and System-Wide coafile
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can place a ``.coarc`` file in your home directory to set certain
user wide settings. Those settings will automatically be taken for all
projects executed with that user.

All settings specified here override only settings given by the system
wide coafile which has the lowest priority. The ``default_coafile`` must
lie in the coala installation directory and is valid for everyone using
this coala installation.

It can be used to define the type of files you usually don't want to lint,
like minified files (e.g. ``*.min.js``) and backup files (e.g. ``*.orig``)::

    ignore = **.min.js, **.orig

Explicit Setting Inheritance
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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
sections without semantically making sense::

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
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Comments are simply done with a preceding ``#``. If you want to use a
``#`` within a value, you can simply escape it:

::

    a_key = a\#value # And a comment at the end!

Any line not containing an unescaped ``=`` is simply appended to the
value of the last key:

::

    a_key = a
    value
    # this is not part of the value
    that /= is
    very long!

Similarly, you can also set a value to multiple keys:
``key_1, key_2 = value`` is equivalent to ``key_1 = value`` and
``key_2 = value`` in separate lines.

As the backslash is the escape character it is recommended to use
forward slashes as path separator even on Windows (to keep relative
paths platform independent), use double-backslashes if you really mean a
backslash in all places.



Now, try it by yourself:

::

    cat .coafile

.. note::

    If you are using Windows, you should use ``type .coafile`` instead!

This should yield something like this:

::

    [cli]
    bears = SpaceConsistencyBear
    files = src/*.c
    use_spaces = True

If you now invoke ``coala`` it will parse this ``.coafile`` from your
current directory. This makes it easy to specify once for your project
what is checked with which bears and make it available to all
contributors.

Feel free to play around with this file. You can either edit it manually
or add/edit settings via ``coala --save ...`` invocations. If you want
coala to save settings every time, you can add ``save = True`` manually
into your ``.coafile``.

Sections
--------

Thats all nice and well but we also have a Makefile for our project we
want to check. So let us introduce another feature of our configuration
syntax: *sections*.

The line ``[cli]`` in the ``.coafile`` implies that everything below
belongs to the special ``cli`` section. You may specify sections when
you enter the settings via the Command Line Interface (CLI). You will
soon learn all about them.  When you don't specify any sections, the
settings will implicitly belong to the ``[cli]`` section.

Next you will see how to specify sections using the command line when
you are running coala. Let's check the line lengths of our Makefile:

::

    coala -S Makefiles.bears=LineLengthBear Makefiles.files=Makefile --save

As you can see, the ``-S`` (or ``--settings``) option allows to specify
arbitrary settings. Settings can be directly stored into a section with
the ``section.setting`` syntax.

By default, the ``LineLengthBear`` checks whether each line contains
``79`` chars or less in a line. To change this value, use the
``max_line_length`` inside the ``.coafile``.

coala will now yield any result you didn't correct last time, plus a new
one for the Makefile. This time coala (or better, the
``LineLengthBear``) doesn't know how to fix the issue but still tries to
provide as much helpful information as possible and provides you the
option to directly open the file in an editor of your choice.

.. note::

    If you want to set a default editor and not be asked for one every time,
    you can simply add ``editor=$editorName`` (i.e. editor=vim) to your
    project's ``.coafile`` and it will automatically open in that one.

.. note::

    If your editor is already open this may not work, because the other
    process will shortly communicate with the existent process and
    return immediately. coala handles this for some editors
    automatically, if yours does not work yet - please file an issue so we
    can include it!

If you changed one file in multiple results, coala will merge the
changes if this is possible.

coala should have appended something like this to your ``.coafile``:

::

    [Makefiles]
    bears = LineLengthBear
    files = Makefile

As you see, sections provide a way to have different configurations for
possibly different languages in one file. They are executed
sequentially.

.. note::

    For a list of configuration options for the bears, take a look at our
    `coala languages <https://coala.io/#/languages>`_ directory.

Auto-applying Results
---------------------

Often you don't want to look at trivial results like spacing issues. For
that purpose coala includes a special setting called ``default_actions``
that allows you to set the action for a bear that shall be automatically
applied on run. We have a command line alias ``--apply-patches`` to make it
easier to use.

By using ``--apply-patches``, the user does not have to press
``2. (A)pply patch`` for applying a patch. Every patch is applied
automatically.
Alternatively, using the setting ``default_actions="*: ApplyPatchAction"``
will automatically apply ``--apply-patches`` on run.

Let's automatically fix Python code. Take a look at our sample Python
code:

::

    $ cat src/add.py

    """
    This is a simple library that provides a function that can add numbers.

    Cheers!
    """



    def add(a,b):
        return a+b;

    import sys

That looks horrible, doesn't it? Let's fix it!

::

    $ coala -S python.bears=PEP8Bear python.files=\*\*/\*.py \
    --apply-patches --save
    # other output ...
    Executing section cli...
    Executing section python...
    [INFO][11:03:37] Applied 'ApplyPatchAction' for 'PEP8Bear'.
    [INFO][11:03:37] Applied 'ApplyPatchAction' for 'PEP8Bear'.

coala would now fix all spacing issues and without bothering you again.

.. note::

    When you try the above example, you may get a warning, saying that all
    settings in the ``cli`` section are implicitly inherited to all
    other sections (if they do not override their values). It also advises
    us to change the name of that section to avoid unexpected behavior.
    The next section explains what it means and how you can avoid
    it.

Setting Inheritance
-------------------
Let's first see what inheritance means.

Before proceeding, rename the ``cli`` section in the ``.coafile`` to
``all`` (we will soon explain the reason behind this change).

Lets add the following section to our ``.coafile``:

::

    [all.TODOS]
    bears = KeywordBear

And execute ``coala`` with the ``-s`` argument which is the same as
``--save``. I recommend setting case insensitive keywords to
``TODO, FIXME`` and case sensitive keywords empty.

After the results we've already seen, we'll see a new informational one
which informs us that we have a TODO in our code.

Did you note that we didn't specify which files to check this time? This
is because all settings, including ``files = src/*.c``, from the ``all``
section (previously called ``cli``) have been inherited in the new
``TODOS`` section that we just added.

You can make a section inherit from any previously defined section using
this syntax:

::

    [parentSection.childSection]

.. note::

    ``cli`` is an internally reserved section name. All of its settings
    are implicitly inherited to every other section by default. It is
    because of this implicit inheritance feature that we are adviced to
    rename the ``cli`` section to something else. Doing so will save us
    from having unexpected values of ``cli`` being implicitly inherited
    into our sections. We strongly suggest renaming it.


Ignoring Issues
---------------

There are several ways to ignore certain issues, so you aren't lost if
any routines yield false positives.

Ignoring Files
~~~~~~~~~~~~~~

coala lets you ignore whole files through the ``ignore`` setting. In
addition to normal globs, coala offers ``**`` to match all directories and
subdirectories:

::

    files = **/*.h
    ignore = **/resources.h

This configuration would include all header (``.h``) files but leaves
out resource headers.

Ignoring Code Inside Files
~~~~~~~~~~~~~~~~~~~~~~~~~~

Sometimes you need finer-graded ignores. Imagine you have a
``LineLengthBear`` that shall not run on some code segments, because you
can't wrap them:

::

    code = "that's checked normally"

    # Ignore LineLengthBear
    unwrappable_string = "some string that is long and would exceed the limit"

You can also skip an area:

::

    # Start ignoring LineLengthBear
    unwrappable_string_2 = unwrappable_string + "yeah it goes even further..."
    another_unwrappable_string = unwrappable_string + unwrappable_string_2
    # Stop ignoring

You can also conditionally combine ignore rules! Bear names will be
split by comma and spaces, invalid bear names like ``and`` will be
ignored.

Also note that in the bear names delimited by commas and spaces, you may
specify glob wildcards that match several bears:

::

    # Start ignoring Line*, Py*
    unwrappable_string_2 = unwrappable_string + "yeah it goes even further..."
    another_unwrappable_string = unwrappable_string + unwrappable_string_2
    # Stop ignoring

In the above example all bears matching the glob `Line*` and `Py*` will
be ignored. You may also specify more complex globs here such as
`# Start ignoring (Line*|P[yx]*)` which will ignore all bears' names which
start with `Line`, `Py`, and `Px`.

::

    # Ignore LineLengthBear and SpaceConsistencyBear
        variable = "Why the heck are spaces used instead of tabs..." + "so_long"

If you put an ``all`` instead of the bear names directly after the
``ignore``/``ignoring`` keyword, the results of all bears affecting
those lines will be ignored.

If you've used another linter in the past, you don't have to change your
pre-existing code with the ``noqa`` keywords to ``ignore`` as the examples
below work as well. If no bears are specified, ``noqa`` will be applicable to
work for all bears.

::

    # noqa
    long_line = "This is a long line ... "

If you wish to specify which bear to use with ``noqa``, as is done
with ``ignore``, you would have to proceed as follows:

::

    # noqa LineLengthBear
    long_line = "This is a long line ... "


Enabling/Disabling Sections
---------------------------

Now that we have sections we need some way to control, which sections
are executed. coala provides two ways to do that:

Manual Enabling/Disabling
~~~~~~~~~~~~~~~~~~~~~~~~~

If you add the line ``TODOS.enabled=False`` to some arbitrary place to
your ``.coafile`` or just ``enabled=False`` into the ``TODOS`` section,
coala will not show the TODOs on every run.

Especially for those bears yielding informational messages which you
might want to see from time to time this is a good way to silence them.

Specifying Targets
~~~~~~~~~~~~~~~~~~

If you provide positional arguments, like ``coala Makefiles``, coala
will execute exclusively those sections that are specified. This will
not get stored in your ``.coafile`` and will take precedence over all
enabled settings. You can specify several targets separated by a space.

What was that TODO again?

Continuing the Journey
----------------------

If you want to know about more options, take a look at our `coala settings
<https://coala.io/help>`_ documentation or with
``coala -h``. If you liked or disliked this tutorial, feel free to drop
us a note at our `bug tracker
<https://github.com/coala/coala/issues>`_ or `mailing list
<https://groups.google.com/forum/#!forum/coala-devel>`_.

If you need more flexibility, know that coala is extensible in many ways
due to its modular design:

-  If you want to write your own bears, take a look at
   `our tutorial <http://coala.io/writingbears>`_.
-  If you want to add custom actions for results, take a look at the
   code in `coalib/results/results_actions <https://github.com/coala/coala/tree/master/coalib/results/result_actions>`__.
-  If you want to have some custom outputs (e.g. HTML pages, a GUI or
   voice interaction) take a look at modules lying in `coalib/output <https://github.com/coala/coala/tree/master/coalib/output>`__.

Happy coding!