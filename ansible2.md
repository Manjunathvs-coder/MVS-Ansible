
Part 2:

Topics:

1. Register and debug
2. Verbocity
3. Pre-task and Post-task
4. Error Handling (ignore_errors: yes)
     a. block
     b. rescue
     c. always
5. Variables
6. Ansible_Vault
7. Change something in the worker node
8. Notify and Handler
9. Template Module
    
<h1>Register</h1>
Register is going to store the data it is nothing but a variable.
debug helps to view the output file with var

```yaml
- hosts: all
  become: yes
  tasks:
    - name: execute the shell cmd
      shell: /usr/bin/date
      register: output
    
    - name: display the output
      debug:
        var: output
```

<h1>Verbocity</h1>

It helps in showcasing the ansible steps in details, it will show if the level is 3 or above

ansible-playbook -i inventary.txt playbook.yaml -vvv ## level 3

```yaml

- hosts: all
  become: yes
  tasks:
    - name: execute the shell cmd
      shell: /usr/bin/date
      register: output
    
    - name: display the output
      debug:
        var: output
        verbosity: 4

```

<h1>Pre task and Post task</h1>

Pre-task - helps in installing the dpendencies befre the main task runs.

task - execute after the pre-task completed

post task - helps in installing after the main task completed.

<h1>Error handling</h1>

1. block
2. rescue
3. always
   
usally if we have an error in between it skips the upcoming tasks, so if we use ignore_errors : yes then it will be autometically ignore the error and execute the upcomming tasks.

```yaml

- hosts: all
  become: yes
  tasks:
    - name: task1
      debug:
        msg: running task1
        
    - name: task2
      debug:
        msg: running task2

    - name: task3
      command: /bin/false
      ignore_errors: yes

    - name: task4
      debug:
        msg: running task4

```
<h3>Block - in case of any error it stops the execution in that step and move to rescue</h3>
<h3>Rescue - executes post Block failure, there is no block then it doesn't execute here</h3>
<h3>Always - it always executes even though we have an errors</h3>

```yaml

- hosts: prod
  become: yes
  tasks:
    - name: executing the tasks
      block:
        - name: task 1
          debug:
            msg: running task 1

        - name: task_error
          command: /bin/false
        
        - name: task 3
          debug:
            msg: running task 3

      rescue:
        - name: execute in case of an ignore_errors
          debug: 
            msg: i got the ignore_errors

        - name: execute in case of an ignore_errors
          command: /bin/false

        - name: execute the 2nd task_error
          debug:
            msg: end error
      always:
        - name: always do this
          debug:
            msg: i have successfully executed this

```

<h2>Variables</h2>

we can store it in vars and re-use inside the code
<h3>we can use vars and vars_files</h3>
<h3>vars_files we can save the variables and use it in the code</h3>

```yaml
- hosts: prod
  become: yes
  vars:
    color: block
    car: bmw
  vars_files:
    sensitive.yaml
  tasks:
    - name: what is my car
      debug:
        msg: my car is {{ car }} and color is {{ color }}. user name is {{ uname }}
      
```

<h2>Ansible-Vault</h2>

<h3> it is used to encrypt the sensitive files with AES256 (Advanced Encryption Standard)</h3>
<h3> ansible-vault encrypt sensitive.yaml</h3>

<h3> ansible-vault decrypt sensitive.yaml</h3>

<h3>ansible-playbook -i inventary.txt playbook.yaml -e "color=red" --ask-vault-password</h3>

<h2>Change something in the worker node</h2>
<h3>we can modify the content of the worker node by using Module : lineinfile</h3>

```yaml
- hosts: prod
  become: yes
  vars:
    new_company: infosys
  tasks:
    - name: replace the file
      lineinfile:
        path: /home/ec2-user/content.txt
        regexp: '^Company:'
        line: 'Company: {{ new_company }}'
```

<h2>Notify and Handlers</h2>
<h3>It executes when there is a change in the execution</h3>

```yaml
- hosts: prod
  become: yes
  vars:
    new_company: infosys
  tasks:
    - name: replace the file
      lineinfile:
        path: /home/ec2-user/content.txt
        regexp: '^Company:'
        line: 'Company: {{ new_company }}'
      notify: trigger
  handlers:
    - name: trigger
      debug: 
        msg: It is executed when there is a change

```

<h1>lininfile: specific content changes in worker node</h1>

```yaml
- hosts: prod
  become: yes
  vars:
    new_company: infosys
  tasks:
    - name: replace the file
      lineinfile:
        path: /home/ec2-user/content.txt
        regexp: '^Company:'
        line: 'Company: {{ new_company }}'
      notify: trigger
  handlers:
    - name: trigger
      debug: 
        msg: It is executed when there is a change
```
