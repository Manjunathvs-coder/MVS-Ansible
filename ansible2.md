
Part 2:

Topics:

1. Register and debug

<h1>Register</h1>

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
