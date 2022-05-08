# [python_pip](#python_pip)

|GitHub|GitLab|
|------|------|
|[![github](https://github.com/mullholland/ansible-role-python_pip/workflows/Ansible%20Molecule/badge.svg)](https://github.com/mullholland/ansible-role-python_pip/actions)|[![gitlab](https://gitlab.com/mullholland/ansible-role-python_pip/badges/master/pipeline.svg)](https://gitlab.com/mullholland/ansible-role-python_pip)|[![quality](https://img.shields.io/ansible/quality/unset)](https://galaxy.ansible.com/mullholland/python_pip)|

description

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
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


## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
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

The machine needs to be prepared in CI this is done using `molecule/default/prepare.yml`:
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





## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

-   [debian9](https://hub.docker.com/r/mullholland/docker-molecule-debian9)
-   [debian10](https://hub.docker.com/r/mullholland/docker-molecule-debian10)
-   [debian11](https://hub.docker.com/r/mullholland/docker-molecule-debian11)
-   [ubuntu1804](https://hub.docker.com/r/mullholland/docker-molecule-ubuntu1804)
-   [ubuntu2004](https://hub.docker.com/r/mullholland/docker-molecule-ubuntu2004)
-   [centos7](https://hub.docker.com/r/mullholland/docker-molecule-centos7)
-   [centos-stream8](https://hub.docker.com/r/mullholland/docker-molecule-centos-stream8)
-   [centos-stream9](https://hub.docker.com/r/mullholland/docker-molecule-centos-stream9)
-   [ubi8](https://hub.docker.com/r/mullholland/docker-molecule-ubi8)
-   [fedora34](https://hub.docker.com/r/mullholland/docker-molecule-fedora34)
-   [fedora35](https://hub.docker.com/r/mullholland/docker-molecule-fedora35)
-   [amazonlinux](https://hub.docker.com/r/mullholland/docker-molecule-amazonlinux)
-   [rockylinux8](https://hub.docker.com/r/mullholland/docker-molecule-rockylinux8)
-   [almalinux8](https://hub.docker.com/r/mullholland/docker-molecule-almalinux8)

The minimum version of Ansible required is 2.10, tests have been done to:

-   The previous versions.
-   The current version.
-   The [devel](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-devel-from-github-with-pip) version.





If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-python_pip/issues)

## [License](#license)

MIT


## [Author Information](#author-information)

[Mullholland](https://github.com/mullholland)

## [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
