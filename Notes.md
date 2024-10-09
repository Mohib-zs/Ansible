"""This is only if your server requires password for sudo priviligies"""
A more secure approach is to store the sudo password using Ansible Vault, which allows you to encrypt sensitive information.
Create an encrypted file for your sudo password:

```ini
ansible-vault create vault.yaml
```

Inside the file, store the password as a variable:

**ansible_become_password: "your_sudo_password"**

In your playbook before tasks
```yaml
- name: Configure nginx web server
  hosts: webserver
  become: yes
  vars_files:
    - vault.yaml
```

```yaml
- name: Configure nginx web server
  hosts: webserver
  become: yes
  vars:
    ansible_python_interpreter: /usr/bin/python     #When python3 is not available, install it using this config, then set python3 default in ansible.cfg
```
interpreter_python = /usr/bin/python3         #In ansible.cfg


[text](https://docs.ansible.com/ansible/2.9/modules/list_of_all_modules.html)