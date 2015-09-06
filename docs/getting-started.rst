Getting started
===============

.. contents::
   :local:

Initial configuration
---------------------

The Docker package from distribution repositories will be installed by default
(on Jessie it means that ``jessie-backports`` repository needs to be available,
which is the default in DebOps). You can install the upstream version of Docker
by setting the ``docker_upstream: True`` variable in Ansible inventory.

If ``debops.pki`` was configured on the host, Docker will automatically listen
on its TCP port for incoming TLS connections, which is by default blocked by
the ``ferm`` firewall. If you don't use firewall or have it disabled, you might
want to set ``docker_tcp`` to ``False`` to disable this behaviour.

Docker manages its own network bridge and ``iptables`` entries. The ``ferment``
Python script will be installed to allow ``ferm`` firewall to reload Docker
firewall rules automatically, however it does not fully support Docker yet, so
be aware of this when you modify the firewall configuration. You can restart
``docker`` daemon to make sure that all firewall rules are set up correctly.

``debops.docker`` relies on configuration managed by ``debops.core``,
``debops.ferm``, and ``debops.pki`` Ansible roles.

Useful variables
----------------

This is a list of role variables which your most likely want to define in
Ansible inventory to customize Docker:

``docker_tcp_allow``
  List of IP addresses or subnets that can connect to Docker daemon remotely
  over TLS.

``docker_admins``
  List of UNIX accounts that have access to Docker daemon socket.

Example inventory
-----------------

To configure Docker on a given remote host, it need to be added to
``[debops_docker]`` Ansible inventory group::

    [debops_docker]
    hostname

Example playbook
----------------

Here's an example playbook that can be used to manage Docker::

    ---
    - hosts: debops_docker
      become: True

      roles:

        - role: debops.docker
          tags: [ 'role::docker' ]

Ansible tags
------------

You can use Ansible ``--tags`` or ``--skip-tags`` parameters to limit what
tasks are performed during Ansible run. This can be used after host is first
configured to speed up playbook execution, when you are sure that most of the
configuration has not been changed.

Available role tags:

``role::docker``
  Main role tag, should be used in the playbook to execute all of the role
  tasks as well as role dependencies.

``type::dependency``
  This tag specifies which tasks are defined in role dependencies. You can use
  this to omit them using ``--skip-tags`` parameter.

``depend-of::docker``
  Execute all ``debops.docker`` role dependencies in its context.

``depend::etc_services:docker``
  Run ``debops.etc_services`` dependent role in ``debops.docker`` context.

``depend::ferm:docker``
  Run ``debops.ferm`` dependent role in ``debops.docker`` context.

``role::docker:config``
  Run tasks related to Docker configuration.

``role::docker:admins``
  Manage access to Docker daemon by UNIX accounts.

