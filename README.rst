.. image:: https://cloud.githubusercontent.com/assets/7521600/15992701/ef245fd4-30ef-11e6-992d-275c5ca7c3a0.jpg

The official documentation for coala
====================================

This is the official documentation for coala, and it is online at https://docs.coala.io.
The coala repository can be found
`here <https://github.com/coala/coala>`__. 

How to build
============

You should run this command before trying to build the documentation:

::

    pip3 install -r docs-requirements.txt

You can test the documentation locally through simply running

::

    make html

in the root directory. This generates _build\html\index.html that you can view
on your browser.

If you want to add new pages, you need to alter the index.rst file in the root
directory. Please read
http://www.sphinx-doc.org/en/stable/markup/toctree.html#toctree-directive for
an explanation of the syntax.
