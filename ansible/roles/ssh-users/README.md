## ssh-users role
This role deploys a defined set of groups, users, and RSA public keys for those users. This role is for the development and debugging phase of the project, I'm sure CHC has established practices for user management.

### Description
Used for granting SSH and sudo access to remote hosts

### When will I invoke this role?
If you want to deploy users and such to remote hosts

### Dependencies
This role is standalone

### Contents
* creates groups from a dict
* creates users from a dict
* creates and validates a new sudoers file
* deploys SSH public keys
* remove users in the remove_users list

### Parameters
- Dict of groups (defaults/main.yml) - can be overridden when needed
- Dict of users (defaults/main.yml) - can be overridden when needed
- ssh public key files - tougher to override as it looks for key files in this role's files dir. Two potential solutions - pull keys in from github or include the authorized_key content in the users dict.
