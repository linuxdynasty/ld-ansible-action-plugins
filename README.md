# ld-ansible-action-plugins
This is a collection of action plugins that I have written and that I am maintaining.

## include_vars.py
This is the rewrite I did of include_vars. **This has been merged into Ansible 2.2**

### Examples
```yaml
# Include vars of stuff.yml into the 'stuff' variable (2.2).
- include_vars:
    file: stuff.yml
    name: stuff

# Conditionally decide to load in variables into 'plans' when x is 0, otherwise do not. (2.2)
- include_vars: file=contingency_plan.yml name=plans
  when: x == 0

# Load a variable file based on the OS type, or a default if not found.
- include_vars: "{{ item }}"
  with_first_found:
   - "{{ ansible_distribution }}.yml"
   - "{{ ansible_os_family }}.yml"
   - "default.yml"

# bare include (free-form)
- include_vars: myvars.yml

# Include all yml files in vars/all and all nested directories
- include_vars:
    dir: 'vars/all'

# Include all yml files in vars/all and all nested directories and save the output in test.
- include_vars:
    dir: 'vars/all'
    name: test

# Include all yml files in vars/services
- include_vars:
    dir: 'vars/services'
    depth: 1

# Include only bastion.yml files
- include_vars:
    dir: 'vars'
    files_matching: 'bastion.yml'

# Include only all yml files exception bastion.yml
- include_vars:
    dir: 'vars'
    ignore_files: 'bastion.yml'
```
