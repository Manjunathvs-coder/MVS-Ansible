
Ansible is a configuration Management Tool
It is a Push based Machanisum

Agent less - Asible will be installed only on Master node.

Pre-requisite - Python should be installed in all the master and worker nodes.

Difference between Ansible vs Terraform:

Aisbible:                                      Terraform:

Configuration management tool      --->      Infrastructure management tool

it works on Procudural language    --->      It works on Declarative Language

Mutable - it can be changed after  --->      Immutable - it can't be changed, it is going to re-install it
installation

it doesn't have any lifecycle management   ----->  It follows lifecycle management as statefile

==========================================================================================================

Ansible-vs-Puppet-vs-Chef-ipcisco.

![Ansible-vs-Puppet-vs-Chef](Ansible-vs-Puppet-vs-Chef-ipcisco.jpg)

============================================================================================================

Inventary file path : /etc/asible/hosts
Config file : /etc/ansible/ansible.cfg

============================================================================================================

Dynamic Inventary.txt

Grouping of inventary.txt prod and dev is grouping the machines, so while configuring something we can choose the specific group of machines

[prod]
ans-worker3 ansible_host=172.31.26.134 ansible_user=ec2-user ansible_private_key_file=/home/ec2-user/work3.pem

[dev]
ans-worker1 ansible_host=172.31.26.47 ansible_user=ec2-user ansible_private_key_file=/home/ec2-user/work1.pem
ans-worker2 ansible_host=172.31.16.225 ansible_user=ec2-user ansible_private_key_file=/home/ec2-user/work1.pem

============================================================================================================

ansible all -i inventary.txt -a date
ansible all -i inventary.txt -a uptime

==============================================================================================================
**states**


