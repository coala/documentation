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

- Moban reads a yaml file (data.yml), this is then rendered into a jinja template
file (jinja files are found within the moban template folder). A “moban.output”
file is then created.

- The template inherits the .jj2 file, which is located in moban.td.

- To use a user defined template, it can be entered within moban.yml.
Moban > moban.cd > moban.yml > template file = base.jj2 (in moban > templates)


Moban Key Features
-----------------

The layout of Moban’s test environment closely matches the layout of the actual
repository structure. This consistency helps to ensure that each file in the
source code has a corresponding test file. Additionally, if any test cases need
to be modified for any reason, they will be easy to locate due to the similar
file structure.

File structure of the tests directory:

tests
|_____core
|_____data_loaders
|_____deprecated
|_____fixtures
|_____integration_tests
|_____jinja2
|_____mobanfile
|_____regression_tests

The core folder includes tests related to context.py, engine, and moban_factory.py.
These tests ensure that the environment variables in context are initialized
correctly, that the jinja2 engine object that Moban creates functions properly,
and that all of the moban_factory functions correctly find the files that are
needed, whether it be templates or actual yml files.

The data_loaders folder checks that the json_loader, the dictionary merge
function, and the yaml_loader all successfully perform their tasks, while
test_overrides ensures that all overridden functions also work.

The fixtures folder contains testing files that are only created on initial run
of the test cases such that the test files are not stored in the production build
of moban.


Why Moban, and How?
-----------------

After Jon's discovery
