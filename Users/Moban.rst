What is Moban?
====================

Description
-----------------

Moban is an open source general purpose static text generator , which can use
other python template engine: mako, handlebars, velocity, haml, slim and
tornado, can read other data format: json and yaml, and can access both template
file and configuration file in any location: zip, git, pypi package, s3, etc.
It is used in coala project to keep documentation consistent across the
documentations of individual libraries in the same organisation. You can find
more documentation on `MobanDocumentation https://moban.readthedocs.io/en/latest/`__

Install ``moban``:

::

    $ pip install moban

CLI arguments:

::

    moban [-h] [-c CONFIGURATION] [-t TEMPLATE] [-o OUTPUT] [-td [TEMPLATE_DIR [TEMPLATE_DIR ...]]]
    [-cd CONFIGURATION_DIR] [-m MOBANFILE] [-g GROUP] [--template-type TEMPLATE_TYPE]
    [-d DEFINE [DEFINE ...]] [-e EXTENSION [EXTENSION ...]] [-f][--exit-code]
    [-V] [-v][template]

Sample usage:

::

    mohan -c [input file(JSON, YAML)] -t [template file] -o [outputfile]
