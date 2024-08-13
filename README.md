# Ansible Collection - iamgini.system_utils

Collection Name: `iamgini.system_utils`

## Installation

Install this collection locally:

```shell
ansible-galaxy collection install iamgini.system_utils
```

## Testing Modules

```shell
$ ansible-navigator run playbooks/create-user.yaml \
    -e "nodes=rhel8" \
    -e "new_user_public_key='your-ssh-public-key'" \
    -u vagrant
```

## Sample Playbooks

Sample playbooks are available in [playbooks](playbooks) directory.

```yaml
---
- name: Create new user
  hosts: "{{ nodes | default('no-such-hosts') }}"
  gather_facts: false
  become: true
  vars:
    new_user_name: devops
    new_user_password: devops
    # new_user_public_key: 'public key string to add'
  tasks:
    - name: Add user
      ansible.builtin.include_role:
        name: add_user
```

## Sharing Collection to Ansible Galaxy

Contribute back to the community !

You can use either the GUI method (browsing the Zip file and upload to Ansible Galaxy) or the CLI method with API token.

### Publishing Ansible Collection using Ansible Playbook

I have an Ansible playbook which will build and publish the Ansible Collection with proper version tag.

```shell
$ ansible-playbook utilities/update-collection.yaml -e "tag=1.0.10"

# or use the Private Automation Hub
$  ansible-playbook utilities/update-collection.yaml -e "tag=0.0.1 server=https://pah.lab.local/api/galaxy/content/published/"
```

### Publishing Ansible Collection Manually

**Configure `ANSIBLE_GALAXY_TOKEN`**

```shell
$ export ANSIBLE_GALAXY_TOKEN='YOUR_ANSIBLE_GALAXY_API_TOKEN'
```

**Building the collection archive**

`ansible-galaxy collection build` command will create the collection archive with version information which you can publish to Ansible Galaxy.

```shell
$ ansible-galaxy collection build
# --force to overwrite if any existing archive with same version

% ls -la *.tar.gz
-rw-r--r--  1 gini  staff  7023  8 Sep 11:12 iamgini-collection_demo_roles_modules-1.0.10.tar.gz
```

**Publish the Collection to Ansible Galaxy**

Make sure you have created the Ansible Galaxy API Token and exported as environment variable `ANSIBLE_GALAXY_TOKEN` before you call the publish command.

```shell
$ ansible-galaxy collection publish \
  ./iamgini-collection_demo_roles_modules-{{ tag }}.tar.gz \
  --api-key $ANSIBLE_GALAXY_TOKEN \
  --ignore-certs
```
