Docker
=========

Installs Docker from docker repo and added users to docker group.

Requirements
------------

Nothing! Just start this role!


Example Playbook
----------------

- name: Install docker
  hosts: staging_servers
  become: true
  roles:
    - role: docker

Author Information
------------------

nodegopher@gmail.com
Nagornov Vyacheslav

