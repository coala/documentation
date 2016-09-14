Bears That Can Suggest And Make Corrections
-------------------------------------------

**Note**: Go through the `Linter Bears
<http://coala.readthedocs.org/en/latest/Users/Tutorials/Linter_Bears.html>`_
documentation before reading this.

Some executables (like ``indent`` or ``autopep8``) can generate a corrected
file from the original. We can use such executables so that coala, using
these bears, can suggest and also make automatic corrections. Here's an
example bear. (GNUIndentBear)

::

    import platform

    from coalib.bearlib.abstractions.Linter import linter
    from coalib.bearlib import deprecate_settings


    @linter(executable="indent" if platform.system() != "Darwin"
                                  else "gindent",
        use_stdin=True,
        output_format='corrected',
        result_message="Indentation can be improved.")
    class GNUIndentBear:
        """
        This bear checks and corrects spacing and indentation via
        the well known Indent utility.
        """

    @staticmethod
    @deprecate_settings(indent_size='tab_width')
    def create_arguments(filename, file, config_file,
                         max_line_length: int=79,
                         use_spaces: bool=True,
                         blank_lines_after_declarations: bool=False,
                         blank_lines_after_procedures: bool=False,
        """
        :param max_line_length:
            Maximum number of characters for a line.
        :param use_spaces:
            True if spaces are to be used, else tabs.
        :param blank_lines_after_declarations:
            Forces blank lines after the declarations.
        :param blank_lines_after_procedures:
            Force blank lines after procedure bodies.
        :param blank_lines_after_commas:
            Forces newline after comma in declaration.
        """

        indent_options = ("--no-tabs" if use_spaces else "--use-tabs",
                      "--line-length", str(max_line_length),
                      "--indent-level", str(indent_size),
                      "--tab-size", str(indent_size), )
        indent_options += (("--blank-lines-after-procedures",)
                          if blank_lines_after_procedures else ("-nbap",))
        indent_options += (("--blank-lines-after-declarations",)
                           if blank_lines_after_declarations else ("-nbad",))
        return (indent_options,)


In the example above, the important line is:

::

    output_format = 'corrected'

This tells the ``linter`` decorator that this bear can suggest corrections.
When we do this, internally a ``diff`` of the original file and the generated
'corrected file' along with some other not-important-for-this-tutorial magic
is used to get the final output (which may be suggestions or
auto-corrections).

Let's try this bear out. Create a new file called ``sample.cpp``. Contents of
``sample.cpp`` are:

::

    #include <iostream>
    int main(){
    if(1 == 1)
    if(2 == 2)
    if(3 != 4)
    cout << "Pun Indented." << endl;

    return 0;
    }

And, run the following command:

::

    coala --bear-dirs=. --bears=GNUIndentBear --files=sample.cpp -s

Make sure that both ``GNUIndentBear.py`` and ``sample.cpp`` are in your current
folder. Also make sure that ``indent`` is installed (**not** the pip package,
but the gnu one which can be installed using your system package manager).

Now, we have a bear that is much more helpful than just a simple Linter Bear!
