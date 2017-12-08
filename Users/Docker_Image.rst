What is Docker?
===============

Docker is a tool designed to make it easier to create, deploy, and run
applications by using containers. Containers allow a developer to package
up an application with all of the parts it needs, like libraries and other
dependencies, and ship it all out as a single package.

With the help of containers, the developer can rest assured that
the application will run on other machines regardless of any
customized settings his machine might have that could differ from the
machine used for writing and testing the code.

Unlike a virtual machine, rather than creating a whole virtual operating
system, Docker allows applications to use the same kernel as the system
that they're running on and only requires applications being shipped
with things not already running on the host computer. This gives a
significant performance boost and reduces the size of the application.

What is a Docker Image and how is it different from a container?
----------------------------------------------------------------

An image is an immutable file which contains required binaries and libraries
needed to make a container and a running instance of an image is called
a container. Images are composed of layers of other images. Images are
created when we run the ``build`` command of Docker and containers are formed
from these images when we use the ``run`` command of Docker. There can be
many containers for the same image.

For more information about Docker see the
`official documentation <https://docs.docker.com/>`__.

Installing Docker
-----------------

Docker installation guide for various operating systems can be found in the
`official Docker installation instructions <https://docs.docker.com/engine/installation/>`__.

.. note::

  Docker images are usually very large. Downloading or pushing them over
  low bandwidth connections can be very slow.


coala as a Docker Image
=======================

We provide a ``coala/base`` docker image for your convenience, that has
dependencies for most official bears already installed.

You can use the ``coala/base`` docker image to perform static code analysis
on your code in the working directory, like this:

::

    docker run -v=$(pwd):/app --workdir=/app coala/base coala --ci

.. seealso::
  See also https://hub.docker.com/r/coala/base/.

.. note::

  The coala Docker image does not support Python 2 analysis.

You can add coala as alias for docker image, like this:

::

  alias coala="docker run -ti -v $(pwd):/app --workdir=/app coala/base coala"

coala on GitLab CI
------------------

You can use the ``coala/base`` docker image to perform static code analysis
on your code with a ``.gitlab-ci.yml``, like this:

::

    check_code:
      image: coala/base
      script:
      - pip install -r requirements.txt
      - coala --ci

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
    script: docker run -v=$(pwd):/app --workdir=/app coala/base coala --ci

.. note::

  For more information about Travis CI configuration, consult the
  `official documentation <https://docs.travis-ci.com/>`__.


coala on Circle CI
------------------

You can use the ``coala/base`` docker image to perform static code analysis
on your code with a ``circle.yml``, like this:

::

    machine:
      services:
        - docker

    test:
      override:
        - docker run -v=$(pwd):/app --workdir=/app coala/base coala --ci

.. note::

  For more information about Circle CI configuration, consult the
  `official documentation <https://circleci.com/docs/>`__.
