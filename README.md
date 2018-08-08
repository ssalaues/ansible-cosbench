# ansible-cosbench
Fork of ksingh7/ansilbe-role-cosbench
=========

Ansible role to install and configure [COSBench](https://github.com/intel-cloud/cosbench) (Cloud Object Storage Benchmarking Tool)

Installation
------------
```$ git clone https://github.com/ssalaues/ansible-cosbench.git```

Customization
--------------
Variable file :  ``ansible-cosbench-role/vars/main.yml``
If you want to install any other version of COSBench , update the following variable
```
cosbench_version: 0.4.2.c4
```

If you want to change the hostname for the target, it can be changed in ``update-hosts/vars/main.yml``

Dependencies
------------
- This role depends on a specific naming convention of hostgroups in your inventory file. So your ansible inventory file should look like this
```
cos1 ansible_host=10.100.2.27   ansible_user=ubuntu zenko=10.100.1.250
cos2 ansible_host=10.100.3.43   ansible_user=ubuntu zenko=10.100.2.53
cos3 ansible_host=10.100.2.59   ansible_user=ubuntu zenko=10.100.2.187
cos4 ansible_host=10.100.1.232  ansible_user=ubuntu zenko=10.100.1.202
cos5 ansible_host=10.100.3.69   ansible_user=ubuntu zenko=10.100.1.33

[cosbench-controller]
cos1

[cosbench-driver]
cos1
cos2
cos3
cos4
cos5

[cosbench:children]
cosbench-controller
cosbench-driver
```
Example Playbook
----------------
Your playbook should look like this

    - hosts: cosbench
      roles:
         - { role: ansible-role-cosbench }

To install cosbench:

```
ansible-playbook -i inventory -b main.yml
```

To only update the target zenko.local hosts

```
ansible-playbook -i inventory -b main.yml --tags "metal"
```

To uninstall it:

```
ansible-playbook -i inventory -b main.yml -e "uninstall=True"
```

License
-------

Apache

Author Information
------------------

Originially created by created [Karan Singh](http://www.ksingh.co.in).


