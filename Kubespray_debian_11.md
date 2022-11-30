## Step 1: Prepare your servers:

```
sudo apt update
sudo apt upgrade
sudo apt install sshpass
```


## Step 2: Prepare your ansible master-machine:

1) Login with your user (not root) and add sudo:

```
usermod -aG sudo pi
```

2) Change your hosts file:

```
sudo nano /etc/hosts
```
```
51.250.111.74   master0
84.252.142.192  worker1
84.252.136.96   worker2
```

3) Create and add keys to remote hosts (from not root user!):

```
ssh-keygen
ssh-copy-id pin@master0
ssh-copy-id pin@worker1
ssh-copy-id pin@worker2
```

4) Clone kubespray and install dependencies:

```
cd ~
git clone https://github.com/kubernetes-sigs/kubespray.git
cd kubespray
sudo apt install python3-pip
sudo pip3 install -r requirements.txt
ansible --version
```

5) Create your directory of inventory:

```
cp -rfp inventory/sample inventory/mycluster
```

6) Change servers in the inventory:

```
sudo nano inventory/mycluster/inventory.ini
```

Example: 

```
# ## Configure 'ip' variable to bind kubernetes services on a
# ## different ip than the default iface
# ## We should set etcd_member_name for etcd cluster. The node that is not a etcd member do not need to set the value, or can set the empty string value.

[all]
master0   ansible_host=51.250.111.74       ansible_user=pin      ansible_sudo_pass=951753
worker1   ansible_host=84.252.142.192      ansible_user=pin      ansible_sudo_pass=951753
worker2   ansible_host=84.252.136.96       ansible_user=pin      ansible_sudo_pass= !vault |
                                                              $ANSIBLE_VAULT;1.2;AES256;dev
                                                              37636561366636643464376336303466613062633537323632306566653533383833366462366662
                                                              6565353063303065303831323539656138653863353230620a653638643639333133306331336365
                                                              62373737623337616130386137373461306535383538373162316263386165376131623631323434
                                                              3866363862363335620a376466656164383032633338306162326639643635663936623939666238
                                                              3161

# ## configure a bastion host if your nodes are not directly reachable
# [bastion]
# bastion ansible_host=x.x.x.x ansible_user=some_user

[kube_control_plane]
master0

[etcd]
master0

[kube_node]
worker1
worker2

[calico_rr]

[k8s_cluster:children]
kube_control_plane
kube_node
calico_rr
```

7) Change settings of the cluster:

```
sudo nano inventory/mycluster/group_vars/k8s-cluster/k8s-cluster.yml
sudo nano inventory/mycluster/group_vars/all/all.yml
```

## Step 3: Create your cluster:

```
ansible-playbook -i inventory/mycluster/inventory.ini --become --user=pin --become-user=root cluster.yml
```

Check your cluster on the master: 

```
sudo kubectl get nodes
```

## Step 4: Turn off ipv6 and add DNS:

Here:

```
sudo nano /etc/modprobe.d/disableipv6.conf
```

Add:

```
install ipv6 /bin/true
```

Here:

```
sudo nano /etc/resolv.conf
```

Add:

```
nameserver 8.8.8.8
nameserver 8.8.4.4
```

## Step 5: Install ingress Nginx:



## Step 6: Install Kubernetes Dashboard:


