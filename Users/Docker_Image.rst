coala as a Docker Image
=======================

We provide a ``coala/base`` docker image for your convenience, that has
dependencies for most official bears already installed.

You can use the ``coala/base`` docker image to perform static code analysis
on your code in the working directory, like this:

::

    docker run --volume=$(pwd):/app --workdir=/app coala/base coala-ci

In bash, an alias is an alternative and usually easier-to-understand or
more significant name for a defined data object.
 
Syntax: ``alias`` "name" ``command``.

Now "name" has the command value.

To run coala from docker using only the ``coala`` command, you can use:

::

 alias coala="docker run -ti -v \`pwd\`:/app --workdir=/app coala/base coala"

.. seealso::
  See also https://hub.docker.com/r/coala/base/.

coala on GitLab CI
------------------

You can use the ``coala/base`` docker image to perform static code analysis
on your code with a ``.gitlab-ci.yml``, like this:

::

    check_code:
      image: coala/base
      script:
      - pip install -r requirements.txt
      - coala-ci

.. note::

  For more information about GitLab CI configuration, consult the
  `official documentation <https://docs.gitlab.com/ce/ci/>`__.

Troubleshooting GitLab CI
-------------------------

You might experience DNS related difficulties with a private GitLab CI setup.
The coala container might not be able to clone the repository if the GitLab
server name is not resolvable.

When this is the case, the most straightforward workaround is to add a
configuration line inside the ``config.toml``
`configuration file <https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/configuration/advanced-configuration.md>`__
for the ``gitlab-ci-multi-runner`` runner:

::

      extra_hosts = ["my-gitlab.example.com:192.168.0.100"]

Please be aware that the most generic ``dns`` setting listed in the
``gitlab-ci-multi-runner`` documentation has been recently added and at
the time of this writing is not available in official builds.

coala on Travis CI
------------------

You can use the ``coala/base`` docker image to perform static code analysis
on your code with a ``.travis.yml``, like this:

::

    language: generic
    services: docker
    script: docker run --volume=$(pwd):/app --workdir=/app coala/base coala-ci

.. note::

  For more information about Travis CI configuration, consult the
  `official documentation <https://docs.travis-ci.com/>`__.
