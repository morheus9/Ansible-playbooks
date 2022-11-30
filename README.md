# Ansible

## Can you speed up your roles with:


- Turn of host_key_checking for stable and secure environment:
```
[defaults]
host_key_checking = False
```

- SSH multiplexing:

The first thing to check is whether the SSH connection re–use works. Since Ansible performs all actions via SSH, any delay in establishing a connection significantly slows down the execution of the playbook as a whole.
<br>In the ansible.cfg add:
```
[ssh_connection]
ssh_args = -o ControlMaster=auto -o ControlPersist=60s
```
Check: 
```ansible test -vvvv -m ping``` 
<br>You should see: 
<br>```SSH: EXEC ssh -vvv -C -o ControlMaster=auto -o ControlPersist=60s... -o ControlPath=/home/ubuntu/.ansible/cp/7c223265ce```


- Enable Pipeling:
```
[ssh_connection]
pipelining = true
```
Check: 
<br>```ansible test -vvv -m ping``` 
<br>You should see ONE ssh call. Not a few.


- Turn off gather_facts:
<br>```gather_facts: no```


- Place the ansible master in the environment closest to the target hosts. For example in the same AWS region.
