packer-arch-aegir
=================

Currently, this is only a Vagrant script that creates an (insecure, as in a password-less root account) Arch Linux Virtualbox. Shortly, this will expand to provision a fully functional LAMP stack with Aegir and Drush ready to use.

The scope is to create an entirely self-contained Drupal dev/dev-testing environment meant for (very) rapid prototyping, proof-of-concept testing, or local development. Expanding this to support client-facing, QA/UAT, or even production-level use? I'm not sure. (Beware the feature creep.) But this is a personal project also meant for me to really understand the current state of a most basic modern web server (read: sans scalability and security, yet) quite literally from the kernel up, including DevOps goodies, like:

- implementing systemd, system-wide and per-user;
- using sockets and D-Bus for standard IPC;
- monitoring processes and threads through cgroups; and
- tracking the entire system -- packages, configurations, and all -- through reproducible and version-controllable snapshots.

## Current Features:

- Pure systemd implementation (no, not even SysV compatibility packages, although systemd can use SysV and LSB scripts)
- 64-bit only (without multilib/32-bit/i686 repositories enabled or packages installed)
- Sub-base Arch Linux installation (i.e. excluding unnecessary base packages like support for Reiser FS or PCMCIA utilities)

## Upcoming Features: (as in within the week)

- Full LAMP stack with Aegir and Drush installed
- A non-root account to execute and own all web-server-related daemons and related sudo privileges
- A non-root user account with an appropriate whitelist of sudo privileges

## Design Principles:

- Simplicity -- minimise complications and complexity.
  - Minimise external dependencies.
  - Avoid deviations from upstream software.
  - Isolate and track all mods and non-default configurations.
- Modernity -- leverage the latest in software.
- Reusability -- parameterize appropriately to provide transparent software that can "just work"™ and be configurable.

## Goals:

- Support of the latest releases of software, namely:
  - Apache 2.4 (Aegir has yet to be fully ported over, among other Drupal oopses)
  - MariaDB 10.0 (as the first RC was just released yesterday)
  - PHP 5.5
  - Drupal 6 and 7 (and 8 very soon afterwards)
- Dropping use of bash in favour of dash (and using only standard non-Bashism scripting)
- Use in a Windows and OS X system (VirtualBox is truly cross-platform, but the provisioning automation and any included host-system interaction is not trivially cross-platform)
- Modular or meta-package architecture (e.g. so it can optionally provision with, or be switched to support, niche support for sites with heavier multimedia requirements or PDF/print-this-page facilities or Java support)

## Considerations and other up-in-the-air's:

- Support for various caching schemes
- Support for multi-user use cases
- Support for use as a non-local, always-on server
