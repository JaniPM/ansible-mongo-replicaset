# ansible-mongo-replicaset
Example to configure MongoDB replica set using Ansible

# Getting started
- Update hosts inventory file with correct mongod virtual machine addresses. 
Make sure primary is the first one on list. One of the nodes is arbiter. 
- Make sure you have ansible.cfg configured with correct host file path and 
ssh key file. E.g. \  
`[defaults]`\
`inventory = ./hosts` \
`private_key_file=<path-to-pem-file>`

# Notes about security
Current implementation enables authentication and uses keyfiles for internal
authentication. The role **security** contains file named "secret". This is the content of the keyfile and is copied to each replica-set member. 

In order to create a key file with a complex pseudo-random 1024 character string run `openssl rand -base64 756 > <path-to-keyfile>`

For an improved production ready security use x.509 certificates instead of keyfiles. More information about internal authentication see MongoDB docs for: [Internal-authentication](https://docs.mongodb.com/manual/core/security-internal-authentication/)

Role **mongo-users** adds example users to database. Usernames and passwords are 
written just for example. Those should be replaced with real ones read from vault.
