Getting started
===============

.. contents::
   :local:

Before using ``debops.iscsi`` role, you should configure an iSCSI Target. It
can be configured either on a dedicated SAN storage host, or using Linux
packages like ``targetcli``, ``tgt`` and others. You can use ``debops.tgt``
role to create a simple iSCSI Target server, however using ``targetcli`` to
setup a LIO-based iSCSI Target might be easier.

Example inventory
-----------------

To configure iSCSI Initiator to connect to remote storage, you should add
a given host to ``[debops_iscsi]`` Ansible group::

    [debops_iscsi]
    hostname

Inventory variables
-------------------

Before configuring the role, you should specify the IQN date and Naming
Authority (by default, ``ansible_domain``) to have consistent IQN naming
scheme. It's best to use the registration date of your domain, you can check it
using ``whois`` command::

    iscsi_iqn_date: '1995-08'
    iscsi_iqn_authority: '{{ ansible_domain }}'

Above variables will be used to create and store IQN base name, available as
``{{ iscsi_iqn }}``. You can use it in your IQN strings, provided that the same
scheme is used on your iSCSI Target hosts.

iSCSI storage should be configured on a separate internal network or VLAN to
provide security. By default, ``debops.iscsi`` discovers iSCSI Targets on all
configured interfaces. To change that, you can specify interface names to use::

    iscsi_interfaces: [ 'eth1', 'vlan300' ]

You need to specify FQDN hostnames or IP addresses of hosts that provide the
storage to discover iSCSI Targets::

    iscsi_portals: [ 'storage.iscsi.{{ ansible_domain }}' ]

You will also want to configure :ref:`iscsi_targets` and
:ref:`iscsi_logical_volumes` to specify what iSCSI Targets to connect to, as
well as how to manage the storage volumes.

Default usernames and passwords for discovery and session authentication can be
found in ``secret/`` directory (see ``debops.secret`` role for more details).
You can change them by modifying the created files and re-running the role.

Example playbook
----------------

Here's an example playbook which uses ``debops.iscsi`` role::

    ---

    - name: Configure iSCSI Initiator
      hosts: debops_iscsi
      sudo: True

      roles:
        - role: debops.iscsi
          tags: iscsi

