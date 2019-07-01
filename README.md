# user_management

Manage your users and groups using ansible. This will aloow you to create a user/group, maintains the user authorized keys and syncs the users and group maintained in yml file. The users and groups database is maintained in a yml file with their status as present or abesent.

### Example:
john.yml:
```
username: "john"
state: absent
full_name: "John Doe"
groups_name: "wheel"
pub_key: "ssh-rsa .... ..."
```


## Usage Examples:
```
git clone https://github.com/rako1980/user_management.git
cd user_management
```
### Create groups:
```
ansible-playbook ./playbooks/create_group.yml -e "groupname=teamusa"
```

### Create users:
```
ansible-playbook ./playbooks/create_user.yml -e "state=present username=mary full_name='Mary Smith' groups_name=teamusa pub_key='ssh-rsa AAAAB..... ...'"
```
Replace above values with appropriately.
### Update Authorized key:
```
ansible-playbook ./playbooks/update_key.yml -e "username=mary pub_key='ssh-rsa ... ...'"
```


### Delete users:
```
ansible-playbook ./playbooks/delete_user.yml -e "username=mary"
```

### Delete groups:
```
ansible-playbooks ./playbooks/delete_group.yml -e "groupname=teamusa"
```

Once the users or groups are created their individual yml files are created. When existing groups are added or removed, or new public key is updated, it will simply update the yaml files for user or group. You can run the standard.yml playbook to sync the user or group to your desired lists of servers that will simply add or remove users or groups based on their state in the file.

