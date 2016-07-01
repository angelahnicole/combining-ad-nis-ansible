# Combining NIS and AD with Ansible

## Overview

This playbook combines joining a machine to an AD domain and an NIS server. The hope is to be able to use NIS accounts but authenticate with Active Directory since the servers that we are currently using are littered with NIS UIDs and GIDs but we want to use AD to authenticate.

So far, only `CentOS 6` and `CentOS 7` machines are supported in this playbook.

## Variable Files

You will need to do a little bit of setup before using this playbook. The first thing to do is to make sure that you have the following variable and host files filled out:

- `group_vars/all.yml`
- `group_vars/vault.yml`
- `hosts`

### all.yml

This has the variables that all hosts will use for the ad, nis, and join roles. There is an example yml file that you template off of. This file also has descriptions of each variable so you know exactly what you are setting.

```yaml
# group_vars/all.yml.example

# ------------------------------------------------------------------------
# ANSIBLE SPECIFIC VARS
# ------------------------------------------------------------------------

# User that ansible will use to log in with
playbook_remote_user: username

# ------------------------------------------------------------------------
# NIS VARS
# ------------------------------------------------------------------------

# The NIS domain name (NOT fqdn)
nis_domain: ntsg

# A list of addresses of NIS servers. You can either specify the master 
# NIS server, NIS slave server/s, or both.
nis_servers:
  - addr: 0.nis.domain.com
  - addr: 1.nis.domain.com

# ... (see group_vars/all.yml.example for more)

```

### vault.yml

You will also need to create a vault.yml file with the following variables inside:

```yaml
# group_vars/vault.yml

vault_ad_user: <AD username>
vault_ad_pass: <AD password>
```

It is recommended that you create this file using `ansible-vault` like so:

```bash
$ ansible-vault create group_vars/vault.yml
```

For more information on using `ansible-vault`, please visit this the ansible documentation: [Ansible Vault](http://docs.ansible.com/ansible/playbooks_vault.html "Ansible's Documentation for Vault") 

### hosts

This, as usual, contains the host information of the machines that will run this playbook (i.e. the inventory)

## Provision the machine(s) in hosts

Before running this playbook, you have to provision the machines in your hosts file in Active Directory in Windows, as I haven't found a way to automate this. All you need to do is add a computer under the AD domain and make it the same name as the hostname of the linux machine.

## Running the playbook

Currently on my todo... still in the process of creating it.

