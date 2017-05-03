nfs
==============

This role is used to deploy nfs.

Inventory file demo
-------------------

```
nfs-1 ansible_ssh_host=10.10.10.11 ansible_ssh_port=3322 ansible_ssh_user=centos
nfs-2 ansible_ssh_host=10.10.10.12 ansible_ssh_port=3322 ansible_ssh_user=centos
nfs-3 ansible_ssh_host=10.10.10.13 ansible_ssh_port=3322 ansible_ssh_user=centos

[cluster1]
nfs-[1:3]

[nfs:children]
cluster1
```

Notice:

* ansible_ssh_host variable in the inventory file is requried for nfs configurations
* We use the group nfs, the group "cluster1" is temporary, you can name it as you want


host_vars
--------------

For example, if your hostname is vagrant1, then create vagrant1.yml in host_vars with the following content:

```
export_list:
	- location: /var/nfs1
	  permission:  *(rw,sync,no_root_squash)
	- location: /var/nfs2
	  permission:  *(rw,sync,no_root_squash)
```

Example Playbook
----------------

```
---
- hosts: nfs
  become: true
  roles:
    - /path/to/nfs/role
```


License
-------

MIT

