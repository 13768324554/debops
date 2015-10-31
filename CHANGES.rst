Changelog
=========

v0.2.1
------

*Unreleased*

- Fail when keyfile has been generated but ciphertext block device is not
  available. [ypid]

v0.2.0
------

*Released: 2015-10-30*

- Major rewrite to allow to create the crypto and filesystem-layer by this
  role. [ypid]

- Wrote initial documentation. [ypid]

- Moved to `DebOps Contrib`_ (the role is still available under
  `ypid.crypttab`_ until it has been fully renamed to something like
  ``debops.cryptsetup``). [ypid]

v0.1.0
------

*Released: 2015-09-07*

- Initial release. [ypid]

.. _ypid.crypttab: https://galaxy.ansible.com/detail#/role/4559
.. _DebOps Contrib: https://github.com/debops-contrib/
