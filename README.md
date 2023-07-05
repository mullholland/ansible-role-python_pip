# [python_pip](#python_pip)

install and configure virtual environments with pip

|GitHub|GitLab|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![github](https://github.com/mullholland/ansible-role-python_pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/mullholland/ansible-role-python_pip/actions)|[![gitlab](https://gitlab.com/opensourceunicorn/ansible-role-python_pip/badges/master/pipeline.svg)](https://gitlab.com/opensourceunicorn/ansible-role-python_pip)|[![quality](https://img.shields.io/ansible/quality/59128)](https://galaxy.ansible.com/mullholland/python_pip)|[![downloads](https://img.shields.io/ansible/role/d/59128)](https://galaxy.ansible.com/mullholland/python_pip)|[![Version](https://img.shields.io/github/release/mullholland/ansible-role-python_pip.svg)](https://github.com/mullholland/ansible-role-python_pip/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/mullholland/ansible-role-python_pip/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true
  vars:
    python_pip_packages:
      - "python-dateutil"

    # pyvenv_command_map:
    #   CentOS-7:
    #     - "python2-pip"
    #     - "python-setuptools"
    #   RedHat-7:
    #     - "python2-pip"
    #     - "python-setuptools"
    #   Amazon-2:
    #     - "python2-pip"
    #     - "python2-setuptools"
    #   default: "python3 -m venv"
    # # yamllint disable-line rule:line-length
    # pyvenv_command: "{{ pyvenv_command_map[ansible_distribution ~ '-' ~ ansible_distribution_major_version] | default(pyvenv_command_map['default'] ) }}"


    python_pip_venvs:
      - name: "fullExample"
        python: "python3"
        path: "/opt"
        packages:
          - "python-dateutil"
        extra_args: "--no-compile"
        state: latest
      - name: "minExample"
        python: "python"
        path: "/opt"
      - name: "mixExample"
        python: "python"
        path: "/opt"
        state: latest

  roles:
    - role: "mullholland.python_pip"
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/mullholland/ansible-role-python_pip/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: true
  gather_facts: true

  roles:
    - role: mullholland.repository_epel

  tasks:
    - name: Update apt cache
      ansible.builtin.apt:
        update_cache: true
      when:
        - ansible_os_family == "Debian"
```


## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/mullholland/ansible-role-python_pip/blob/master/defaults/main.yml):

```yaml
---
# WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour
# with the system package manager. It is recommended to use a virtual environment
# instead: https://pip.pypa.io/warnings/venv
# For example the variables `python_pip_venvs` down below
# Define pip packages
python_pip_packages: []
#  - "python-dateutil"
#  - "python-dateutil==0.11"
#  - "python-dateutil>=1.1,<=2.1"
#  - "python-dateutil>=1"
python_pip_packages_group: []
python_pip_packages_host: []

# Update pip package before installing packages
python_pip_update: true

python_pip_venvs: []
#  - name: "fullExample"         # required
#    python: "python"            # required
#    path: "/opt"                # required
#    packages:                   # optional => default(omit)
#      - "python-dateutil"
#    extra_args: "--no-compile"  # optional => default(omit)
#    state: latest               # optional => default("present")
#  - name: "minExample"
#    python: "python"
#    path: "/opt"
#  - name: "mixExample"
#    python: "python"
#    path: "/opt"
#    state: latest
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/mullholland/ansible-role-python_pip/blob/master/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://mullholland.net) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/mullholland/ansible-role-python_pip/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/repository/docker/mullholland/docker-centos-systemd/general)|all|
|[Amazon](https://hub.docker.com/repository/docker/mullholland/docker-amazonlinux-systemd/general)|Candidate|
|[Fedora](https://hub.docker.com/repository/docker/mullholland/docker-fedora-systemd/general)|all|
|[Ubuntu](https://hub.docker.com/repository/docker/mullholland/docker-ubuntu-systemd/general)|all|
|[Debian](https://hub.docker.com/repository/docker/mullholland/docker-debian-systemd/general)|all|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-python_pip/issues)

## [License](#license)

[MIT](https://github.com/mullholland/ansible-role-python_pip/blob/master/LICENSE).

## [Author Information](#author-information)

[Mullholland](https://mullholland.net)

Please consider [sponsoring me](https://github.com/sponsors/mullholland).
