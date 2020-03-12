What is Tox?
===============

tox is a generic virtualenv management and test command line tool you can use
for:

- checking your package installs correctly with different Python versions and
  interpreters
- running your tests in each of the environments, configuring your test tool
  of choice
- acting as a frontend to Continuous Integration servers, greatly reducing
  boilerplate and merging CI and shell-based testing.

taken from `tox.readthedocs.io
<https://tox.readthedocs.io/en/latest/>`_.

Basic example.
----------------------------------------------------------------
First, install tox with pip install tox. Then put basic information about
your project and the test
environments you want your project to run in into a tox.ini file residing
right next to your setup.py file:

::

    # content of: tox.ini , put in same dir as setup.py
    [tox]
    envlist = py27,py36
    [testenv]
    deps = pytest # install pytest in the virtualenv where commands
    will be executed
    commands =
    # whatever extra steps before testing might be necessary
    pytest # or any other test runner that you might use
    
.. note::

    You can also try generating a tox.ini file automatically, by running
    tox-quickstart and then answering a few simple questions.
    To sdist-package, install and test your project against Python2.7 and
    Python3.6, just type:

::

    tox
    
.. note::

    and watch things happening (you must have python2.7 and python3.6 
    installed in your environment otherwise you will see errors). When
    you run tox a second time you’ll note that it runs much faster
    because it keeps track of virtualenv details and will not recreate or
    re-install dependencies.You also might want to checkout tox configuration
    and usage examples to get some more ideas.

Sections
--------
The ``tox.ini`` file has a number of top level sections defined by ``[ ]``
and subsections within those. For complete documentation
on all subsections inside of a tox section please refer to the tox
documentation.

- ``tox`` : This section contains the ``envlist`` which is used to create
    our dynamic matrix. Refer to the `section here <http://tox.readthedocs.io/
    en/latest/config.html#generating-environments-conditional-settings>`_ for
    more information on how the ``envlist`` works.

- ``purge`` : This section contains commands that only run for scenarios
    that purge the cluster and redeploy. You'll see this section being reused in
  ``testenv``with the following syntax: ``{[purge]commands}``

- ``update`` : This section contains commands taht only run for scenarios
    that
    deploy a cluster and then upgrade it to another Ceph version.

- ``testenv`` : This is the main section of the ``tox.ini`` file and is run
    on every scenario. This section contains many *factors* that define
    conditional settings depending on the scenarios defined in the 
    ``envlist``.
    For example, the factor``centos7_cluster`` in the ``changedir`` subsection
    of ``testenv`` sets the directory that tox will change do when that factor
    is selected. This is an important behavior that allows us to use the same
  ``tox.ini`` and reuse commands while tweaking certain sections per testing
    scenario.

Modifying or Adding environments
--------------------------------

The tox environments are controlled by the ``envlist`` subsection of the
``[tox]`` section. Anything inside of ``{}`` is considered a *factor* and
will be included
in the dynamic matrix that tox creates. Inside of ``{}`` you can include
a comma separated list of the *factors*. Do not use a hyphen (``-``) as part
of the *factor* name as those are used by tox as the separator between
different factor sets.

For example, if wanted to add a new test *factor* for the next Ceph
release of luminious this is how you'd accomplish that. Currently, the first
factor set in our ``envlist``
is used to define the Ceph release (``{jewel,kraken,rhcs}-...``). To add
luminous you'd change that to look like ``{luminous,kraken,rhcs}-...``.
In the ``testenv`` section
this is a subsection called ``setenv`` which allows you to provide environment
variables to the tox environment and we support an environment variable
called ``CEPH_STABLE_RELEASE``.
To ensure that all the new tests that are created by adding the luminous
*factor* you'd do this in that section:
``luminous: CEPH_STABLE_RELEASE=luminous``.

Note

For more information about Tox configuration, consult the
`official documentation <https://tox.readthedocs.io/en/latest/>`_.
