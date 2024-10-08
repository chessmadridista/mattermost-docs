Deploy Mattermost via Docker
==============================

.. include:: ../_static/badges/allplans-selfhosted.rst
  :start-after: :nosearch:

Install Docker
---------------

If you don't have Docker installed, follow the instructions below based on your operating system:

.. tab:: macOS

  Install `Docker for Mac <https://docs.docker.com/installation/mac/>`__.

.. tab:: Windows 10

  Install `Docker for Windows <https://docs.docker.com/installation/windows/>`__.

.. tab:: Ubuntu

  Follow the `Install Docker Engine on Ubuntu <https://docs.docker.com/engine/install/ubuntu/>`__ documentation, or you can use the Docker package from the Ubuntu repositories:

  .. code-block:: sh

    sudo apt update
    sudo apt install docker.io
    sudo systemctl start docker

.. tab:: Fedora

  Follow the `Install Docker Engine on Fedora <https://docs.docker.com/engine/installation/linux/fedora/>`__ documentation, or you can use the Moby package (Moby is the FOSS upstream project to Docker) from the Fedora repositories:

  .. code-block:: sh

    sudo dnf install moby-engine
    sudo systemctl start docker

.. _Deploy Mattermost on Docker:

Deploy Mattermost on Docker for production use
----------------------------------------------

.. include:: common-prod-deploy-docker.rst
  :start-after: :nosearch:

Upgrade from ``mattermost-docker``
-----------------------------------

The `mattermost-docker <https://github.com/mattermost/mattermost-docker>`__ GitHub repository is deprecated. Visit the `mattermost/docker <https://github.com/mattermost/docker>`_ GitHub repository to access the official Docker deployment solution for Mattermost.

To migrate from an existing ``mattermost/mattermost-prod-app`` image, we recommend migrating to either ``mattermost/mattermost-enterprise-edition`` or ``mattermost/mattermost-team-edition`` images, which are the official images supported by Mattermost. These images support PostgreSQL 11+ databases, which we know has been a long-running challenge for the community, and you will not lose any features or functionality by moving to these new images.

For additional help or questions, please refer to `this issue <https://github.com/mattermost/mattermost-docker/issues/489>`__.

Installing a different version of Mattermost
--------------------------------------------

1. Shut down your deployment.

2. Run ``git pull`` to fetch any recent changes to the repository, paying attention to any potential ``env.example`` changes.

3. Adjust the ``MATTERMOST_IMAGE_TAG`` in the ``.env`` file to point your desired `enterprise <https://hub.docker.com/r/mattermost/mattermost-enterprise-edition/tags?page=1&ordering=last_updated>`__ or `team <https://hub.docker.com/r/mattermost/mattermost-team-edition/tags?page=1&ordering=last_updated>`__ image version.

4. Redeploy Mattermost.

Troubleshooting your production deployment
-------------------------------------------

Docker
~~~~~~

If deploying on an M1 Mac and encountering permission issues in the Docker container, `redo the third step <#create-the-required-directores-and-set-their-permissions>`__ and skip this command:

.. code-block:: sh

  sudo chown -R 2000:2000 ./volumes/app/mattermost

If having issues deploying on Docker generally, ensure the docker daemon is enabled and running:

.. code-block:: sh

  sudo systemctl enable --now docker

To remove all data and settings for your Mattermost deployment:

.. code-block:: sh

  sudo rm -rf ./volumes

PostgreSQL
~~~~~~~~~~~

You can change the Postgres username and/or password (recommended) in the ``.env`` file.

TLS & NGINX
~~~~~~~~~~~~

For an in-depth guide to configuring the TLS certificate and key for Nginx, please refer to `this document in the repository <https://github.com/mattermost/docker/blob/main/docs/issuing-letsencrypt-certificate.md>`__.

Further help
~~~~~~~~~~~~~

If you encounter other problems while installing Mattermost, please refer to our :doc:`troubleshooting guide </install/troubleshooting>`.

Trial Mattermost using Docker Preview
--------------------------------------

Looking to a way to evaluate Mattermost in a non-production environment using Docker? We recommend using the `Mattermost Docker Preview Image <https://github.com/mattermost/mattermost-docker-preview>`_ to install Mattermost in Preview Mode. 

See the :doc:`trial Mattermost using Docker </install/trial-mattermost-using-docker>` documentation for details.