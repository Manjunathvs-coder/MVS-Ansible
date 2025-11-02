
Part 2:

Topics:

1. Register and debug
2. Verbocity
3. Pre-task and Post-task
4. Error Handling (ignore_errors: yes)

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
