configure_master
=========

Configures master for k8s: kubeadm init and compies join command.

Requirements
------------

Nothing! Just start this role!

Role Variables
--------------

Defaults:
```
cidr: 10.244.0.0/16
# for calico: cidr: 192.168.0.0/16
```
Example Playbook
----------------
```
    - hosts: servers
      roles:
         - role: configure_master
```
Author Information
------------------

nodegopher@gmail.com
Nagornov Vyacheslav
