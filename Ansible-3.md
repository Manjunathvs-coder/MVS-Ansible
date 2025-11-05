
<h1>Topics</h1>
<h3>1. Ansible_facts</h3>
<h3>2. delegate_to and Local_host (local_action: command touch text.yaml)</h3>
<h3>3. aync - Maximum time the task can run, if exceeds it gets fail</h3>
<h3>4. poll</h3> 

poll = 0 - it executes all the tasks concurently, it doesn't wait for each task to complete
poll > 0 - it helps in avoiding the connection timeouts

<h3>serial</h3> 
It is going to execute the tasks batch wise.
if we have 4 machines and 2 tasks, if we give serial 2, then first two machines executes 1st task and followed by 2nd task. same for 2nd set of machines
ansible-config init -disabled > ansible.cfg

<h3>fork</h3>
<h4>we have defone fork in asible.cfg file, it is going to esablish the connetion at a time based on the fork size</h4>

<h2>ansible-facts</h2>
it is used to get the information about the worker nodes, based on that we can segrigate which installation commands we need to use

```yaml
- hosts: all
  become: yes
  tasks:
    - name: getting ansible fcats
      debug:
        vars: ansible-facts
```

<h2>Delegate_to</h2>h2>
to run something on the dedicated machine by keeping the IP address

```yaml
- hosts: all
  become: yes
  tasks:
    - name: task1
      debug:
        msg: running the 1st task
    - name: task2
      debug:
        msg: running 2nd task
      delegate_to:
```

<h2>Local_host</h2>
to run something on the local machine

```yaml
- hosts: all
  become: yes
  tasks:
    - name: task1
      debug:
        msg: running the 1st task
    - name: task2
      local_action: command touch text.yaml
```

<h2>async</h2>

we can set the timelimt to run the specific task, if it goes beyond the timeline task is going to get fail.

```yaml
- hosts: all
  become: yes
  tasks:
    - name: running task1
      command: /bin/sleep 4
      async: 2
    
    - name: running 2nd task
      command: /bin/sleep 10
      async: 5
```
