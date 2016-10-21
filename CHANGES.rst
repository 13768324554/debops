.. _golang__ref_changelog:

Changelog
=========

.. include:: includes/all.rst

**debops.golang**

This project adheres to `Semantic Versioning <http://semver.org/spec/v2.0.0.html>`__
and `human-readable changelog <http://keepachangelog.com/en/0.3.0/>`__.

The current role maintainer_ is drybjed.


`debops.golang master`_ - unreleased
------------------------------------

.. _debops.golang master: https://github.com/debops/ansible-golang/compare/v0.1.0...master

Changed
~~~~~~~

- Update documentation and Changelog. [drybjed_]


debops.golang v0.1.0 - 2016-06-28
---------------------------------

Changed
~~~~~~~

- Role rewrite and first release.

  The hard dependency on debops.backporter_ role has been removed, now role
  uses debops.apt_preferences_ to install Go packages from backports on
  older OS releases. [drybjed_]
