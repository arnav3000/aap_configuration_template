# DevConf 2023 - Good Practices and Security for your Ansible Automation Platform-2

### Pre-requisites

1) Running 3 VMs(1 controller, 1 DB, 1 automationhub) for RHEL-8.6 
2) ssh keys generated and exchagned in all 3 mahcines
3) Run this as a root user
4) Once your VM's are running, Replace the vault files with your own with these variables:

```yaml
---
cloud_token: 'this is the one from console.redhat.com'
offline_token: 'this is the one linked below about api token'
rh_username: 'redhat user login (this is used to attach your subs to controller)'
rh_password: 'password for redhat account'
root_machine_pass: 'password for root user on builder (if not root user more changes will need to be made)'
ah_token_password: 'this will create and use this password can be generated'
controller_api_user_pass: 'this will create and use this password can be generated'
controller_pass: 'admin account pass for controller, if none is given it will default to Password1234!'
ah_pass: 'hub admin account pass, if none is given it will default to Password1234!'
vault_pass: 'the password to decrypt this vault'
...
```
### To run this on Open TLC environment use below command :

1) Create new vaulted values with username and passwords for vaults and replace the values in vaults/opentlc.yml file

`ansible-playbook --vault-id vaults/opentlc.yml -i inventory_opentlc.yml -l dev playbooks/controller_config_opentlc.yml --ask-vault-pass -e "env=opentlc" -e "no_log=false"`

## Install and configure Controller and Hub

`ansible-playbook -i inventory_dev.yml -l dev playbooks/install_configure.yml --ask-vault-pass -e "env=dev"`

Acquire your token at [redhat api](https://access.redhat.com/management/api/) see [access article](https://access.redhat.com/articles/3626371)

### 
Based on https://github.com/redhat-cop/aap_configuration_template



