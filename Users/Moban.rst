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
more detailed documentation on `Moban Documentation <https://moban.readthedocs.io/en/latest/>`_.

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

Moban statically generates text based on an input file and an given template, which
can be used to modify all configuration files of an entire repository.

Moban Structure
-----------------

Cathlin's section

Moban Key Features
-----------------

(based on test cases) Christopher's section

Why Moban, and How?
-----------------

After Jon's discovery
