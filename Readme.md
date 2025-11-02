
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
<h2>states</h2>

present - install
absent  -  uninstall
startted  -  start
restartted  -  restart
stopped - stop

<h1>Modules</h1>

i = inventary file
b = become yes
m = module
a = argument

<h3>Adhoc Commands</h3> Single line commands

1. ansible dev -i inventary.txt -m yum -a "name=httpd state=present" -b
2. ansible dev -i inventary.txt -m service -a "name=httpd state=started" -b
3. ansible dev -i inventary.txt -m copy -a "src=index.html dest=/var/www/html" -b

<h2>Playbook</h2>

httpd playbook

```yaml
- hosts: prod
  become: yes
  tasks:
    - name: install httpd
      yum:
        name: httpd
        state: present
    - name: start the service
      service:
        name: httpd
        state: started
    - name: Transfer HTML file
      copy:
        src: index.html
        dest: /var/www/html

ansible-playbook -i inventary.yaml playbook.yaml --syntax-check

<h2>loop and Jinja Template </h2>

```yaml
- hosts: prod
  become: yes
  tasks:
    - name: install multiple applications
      yum:
        name: {{ item }} #jinja
        state: absent
      loop:
        - mysql
        - unzip
        - httpd
---

- hosts: prod
  become: yes
  tasks:
    - name: Print Statement
      debug:
        msg: Running 1st task

...

