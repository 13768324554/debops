Changelog
=========

v0.1.0
------

*Unreleased*

- Add Changelog. [drybjed]

- Change default NFS filesystem type from ``nfs4`` to ``nfs``, system
  automatically picks the correct type. [drybjed]

- Add a way to manage entries in ``/etc/hosts``. [drybjed]

- Add a task that allows to copy custom files from Ansible Controller, list of
  files is configurable using Ansible inventory. [drybjed]

- Add support for setting default system-wide locale. [drybjed]

- Add option to configure system-wide ``editor`` alternative. [drybjed]

- Tag various tasks for convenient use. [drybjed]

- Ensure mount directories exist when manually mounted. [ypid]

- Add kernel parameter configuration and shared memory configuration.

  Amount of shared memory limits starting with Linux kernel 3.16 is ridiculusly
  high by default. This configuration limits the shared memory size to
  reasonable amounts depending on available system RAM. More information:
  https://git.kernel.org/cgit/linux/kernel/git/mhocko/mm.git/commit/include/uapi/linux/shm.h?id=060028bac94bf60a65415d1d55a359c3a17d5c31
  [drybjed]

