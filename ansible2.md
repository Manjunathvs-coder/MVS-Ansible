
Part 2:

Topics:

1. Register and debug

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
