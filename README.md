# Ansible role [filesystem](https://galaxy.ansible.com/ui/standalone/roles/buluma/filesystem/documentation)

Make filesystems.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-filesystem/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-filesystem/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-filesystem.svg)](https://github.com/buluma/ansible-role-filesystem/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-filesystem.svg)](https://github.com/buluma/ansible-role-filesystem/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-filesystem.svg)](https://github.com/buluma/ansible-role-filesystem/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/filesystem)](https://galaxy.ansible.com/ui/standalone/roles/buluma/filesystem/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-filesystem/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: buluma.filesystem
      filesystem_list:
        - dev: disk_1
          fstype: ext4
        - dev: disk_2
          fstype: ext3
          opts: -cc
        - dev: disk_3
          state: absent
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-filesystem/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: true
  gather_facts: false

  roles:
    - role: buluma.bootstrap

  tasks:
    - name: Make disk image
      command: truncate -s 16M "{{ item }}"
      args:
        creates: "{{ item }}"
      loop:
        - disk_1
        - disk_2
        - disk_3
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-filesystem/blob/master/defaults/main.yml):

```yaml
---
# defaults file for filesystem

# If not specified in the `filesystem_list`, use this filesytem type.
filesytem_default_filesystem: ext4

# A list of filesytems to manage.
filesystem_list: []

# For example:
# filesystem_list:
#   - dev: /dev/sdb1
#     fstype: ext4
#   - dev: /dev/sdb2
#     fstype: ext3
#     opts: -cc
#   - dev: /dev/sdb3
#     state: absent
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-filesystem/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-filesystem/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[Alpine](https://hub.docker.com/r/buluma/alpine)|all|
|[Amazon](https://hub.docker.com/r/buluma/amazonlinux)|all|
|[Debian](https://hub.docker.com/r/buluma/debian)|all|
|[EL](https://hub.docker.com/r/buluma/enterpriselinux)|8, 9|
|[Fedora](https://hub.docker.com/r/buluma/fedora)|all|
|[opensuse](https://hub.docker.com/r/buluma/opensuse)|all|
|[Ubuntu](https://hub.docker.com/r/buluma/ubuntu)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-filesystem/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-filesystem/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-filesystem/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)
