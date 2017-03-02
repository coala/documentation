Shell Autocompletion
====================

If you're using ``bash`` or ``zsh`` you can set them up to have tab completion
for coala arguments and bear names.

Install ``argcomplete``:

::

    $ pip install argcomplete

After this you have to either activate it
`globally <https://github.com/kislyuk/argcomplete#activating-global-completion>`__
or modify your configuration.

If you're using ``bash``, add the following to your ``.bashrc``:

::

    eval "$(register-python-argcomplete coala)"

If you're using ``zsh``, add the following to your ``.zshrc``:

::

    autoload bashcompinit
    bashcompinit
    eval "$(register-python-argcomplete coala)"
