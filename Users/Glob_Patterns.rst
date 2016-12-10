Glob - Extended unix style pathname expansion
=============================================

Using Glob Patterns
-------------------

Suppose you want ``SpaceConsistencyBear`` to perform an analysis on a file
``first.c``, you should use the command:
::

    coala --files=src/first.c --bears=SpaceConsistencyBear --save

.. note::

    If you don't know the functions of a bear or how to perform the analysis
    with a bear, you should go through `Tutorial
    <http://coala.readthedocs.io/en/latest/Users/Tutorial.html>`_ first.

Now, if you want all the ``.c`` files in a specific directory to be analysed,
you can take help of glob patterns.
::

    coala --files='src/*.c' --bears=SpaceConsistencyBear --save

Here, ``*.c`` matches all ``.c`` files in the ``src`` directory.
Going further, if you want all ``.c`` as well as ``.java`` files to
be analysed:
::

    coala --files='src/*.(java|c)' --bears=SpaceConsistencyBear --save

If you want your ``files`` argument to match all directories and
subdirectories, you can use ``**`` glob pattern for that.
::

    files = **/*.c

.. note::

    While using ``files = **/*.c``, since we have used ``/`` in the glob
    pattern, all ``.c`` files at least one subdirectory below the root
    directory will be matched.


In coala, files and directories are specified by file name. To allow
input of multiple files without requiring a large number of filenames,
coala supports a number of wildcards. These are based on the unix-style
glob syntax and they are *not* the same as regular expressions.

.. note::

    Any glob that does not start with a ``/`` in Linux or a drive letter
    ``X:`` in Windows will be interpreted as a relative path. Please use comma
    separated values instead of absolute path globs that start with a
    glob expression.

Syntax
------

The special characters used in shell-style wildcards are:

+-------------------+---------------------------------------------------------+
| PATTERN           | MEANING                                                 |
+===================+=========================================================+
| ``[seq]``         | Matches any character in seq. Cannot be empty. Any      |
|                   | special character loses its special meaning in a set.   |
+-------------------+---------------------------------------------------------+
| ``[!seq]``        | Matches any character not in seq. Cannot be empty. Any  |
|                   | special character loses its special meaning in a set.   |
+-------------------+---------------------------------------------------------+
| ``(seq_a|seq_b)`` | Matches either sequence_a or sequence_b as a whole. More|
|                   | than two or just one sequence can be given.             |
+-------------------+---------------------------------------------------------+
| ``?``             | Matches any single character.                           |
+-------------------+---------------------------------------------------------+
| ``*``             | Matches everything but the directory separator.         |
+-------------------+---------------------------------------------------------+
| ``**``            | Matches everything.                                     |
+-------------------+---------------------------------------------------------+

.. note::

    If you're looking for a negation pattern to exclude paths, check out the
    ``--ignore`` argument or ``ignore`` .coafile option `here
    <http://coala.readthedocs.io/en/latest/Users/Tutorial.html#ignoring
    -issues>`_.

Examples
--------

``[seq]``
~~~~~~~~~

    Matches any character in seq. Cannot be empty. Any special character
    loses its special meaning in a set.

Opening and closing brackets can be part of a set, although closing
brackets have to be placed at the first position.

::

    >>> from coalib.parsing.Globbing import fnmatch
    >>> fnmatch("aaa", "a[abc]a")
    True
    >>> fnmatch("aaa", "a[bcd]a")
    False
    >>> fnmatch("aaa", "a[a]]a")
    False
    >>> fnmatch("aa]a", "a[a]]a")
    True
    >>> fnmatch("aaa", "a[]abc]a")
    True
    >>> fnmatch("aaa", "a[[a]a")
    True
    >>> fnmatch("a[a", "a[[a]a")
    True
    >>> fnmatch("a]a", "a[]]a")
    True
    >>> fnmatch("aa", "a[]a")
    False
    >>> fnmatch("a[]a", "a[]a")
    True

``[!seq]``
~~~~~~~~~~

    Matches any character not in seq. Cannot be empty. Any special
    character loses its special meaning in a set.

::

    >>> fnmatch("aaa", "a[!a]a")
    False
    >>> fnmatch("aaa", "a[!b]a")
    True
    >>> fnmatch("aaa", "a[b!b]a")
    False
    >>> fnmatch("a!a", "a[b!b]a")
    True
    >>> fnmatch("a!a", "a[!]a")
    False
    >>> fnmatch("a[!]a", "a[!]a")
    True

``(seq\_a\|seq\_b)``
~~~~~~~~~~~~~~~~~~~~

    Matches either sequence\_a or sequence\_b as a whole. More than two
    or just one sequence can be given.

Parentheses cannot be part of an alternative, unless they are escaped by
brackets. Parentheses that have no match are ignored as well as
``|``-separators that are not inside matching parentheses.

::

    >>> fnmatch("aXb", "a(X|Y)b")
    True
    >>> fnmatch("aYb", "a(X|Y)b")
    True
    >>> fnmatch("aZb", "a(X|Y)b")
    False
    >>> fnmatch("aXb", "(a(X|Y)b|c)")
    True
    >>> fnmatch("a", "a|b")
    False
    >>> fnmatch("a|b", "a|b")
    True
    >>> fnmatch("(aa", "(a(a|b)")
    True
    >>> fnmatch("a(a", "(a(a|b)")
    False
    >>> fnmatch("a(a", "(a[(]a|b)")
    True
    >>> fnmatch("aa", "a()a")
    True
    >>> fnmatch("", "(abc|)")
    True

``?``
~~~~~

    Matches any single character.

::

    >>> fnmatch("abc", "a?c")
    True
    >>> fnmatch("abbc", "a?c")
    False
    >>> fnmatch("a/c", "a?c")
    True
    >>> fnmatch("a\\c", "a?c")
    True
    >>> fnmatch("a?c", "a?c")
    True
    >>> fnmatch("ac", "a?c")
    False

``\*``
~~~~~~

    Matches everything but the directory separator.

.. note::

    The directory separator is platform specific. ``/`` is never
    matched by ``\*``. ``\\`` is matched on Linux, but not on Windows.

::

    >>> fnmatch("abbc", "a*c")
    True
    >>> fnmatch("a/c", "a*c")
    False
    >>> fnmatch("ac", "a*c")
    True

``\*\*``
~~~~~~~~

    Matches everything.

::

    >>> fnmatch("abbc", "a**c")
    True
    >>> fnmatch("a/c", "a**c")
    True
