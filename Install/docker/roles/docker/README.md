Docker
=========

Installs Docker from docker repo and added users to docker group.

Role Variables
--------------
Defaults:
# turn on "docker prune" job in the cron (every month).
```
add_prune_job: false
```
# turn off "docker prune" job in the cron (every month).
```
delete_prune_job: false  
```
Example Playbook
----------------
```
- name: Install docker
  hosts: staging_servers
  become: true
  roles:
    - role: docker
```
Author Information
------------------

nodegopher@gmail.com
Nagornov Vyacheslav

