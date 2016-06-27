# Combining NIS and AD with Ansible

## Overview

This playbook combines joining a machine to an AD domain and an NIS server. The hope is to be able to use NIS accounts but authenticate with Active Directory since the servers that we are currently using are littered with NIS UIDs and GIDs but we want to use AD to authenticate.

## Variable Files

You will need to do a little bit of setup before using this playbook. The first thing to do is to make sure that you have the following variable and host files filled out:

- `group_vars/all.yml`
- `group_vars/vault.yml`
- `hosts`

### all.yml

This has the variables that all hosts will use for the ad, nis, and join roles. There is an example yml file that you template off of.

```yaml
# group_vars/all.yml.example
nis_domain: mynisdomain
ntp_server: mynisdomain.com
ad_domain: ADDOMAIN.COM
# be sure to include these variables in your own group_vars/vault.yml file:
# vault_nis_servers:
#   - ip: <nis slave/server ip address>
#   - ip: <nis slave/server ip address>
#   - ip: <nis slave/server ip address>
#   <and so on>
# vault_ad_cfc_user: <cfc user name>
# vault_ad_cfc_pass: <cfc password>
```

### vault.yml

As the all.yml.example comments allude, you will need to create a vault.yml file with the following variables inside:

```yaml
# group_vars/vault.yml
vault_nis_servers:
  - ip: "<nis slave/server ip address>"
  - ip: "<nis slave/server ip address>"
  - ip: "<nis slave/server ip address>"
vault_ad_cfc_user: "<cfc user name>"
vault_ad_cfc_pass: "<cfc password>"
```

It is recommended that you create this file using `ansible-vault` like so:

```bash
$ ansible-vault create group_vars/vault.yml
```

For more information on using `ansible-vault`, please visit this the ansible documentation: [Ansible Vault](http://docs.ansible.com/ansible/playbooks_vault.html "Ansible's Documentation for Vault") 

### hosts

This, as usual, contains the host information of the machines that will run this playbook (i.e. the inventory)

## Running the playbook

Currently on my todo... still in the process of creating it.

