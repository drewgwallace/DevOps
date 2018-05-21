# Ansible Playbook



## Purpose
  Execute this play against a supported server, it will install dependencies, create an "ansible" user and group, then place the executing machine's SSH public key into the target's trusted keystore.
  
----

## Execution
    sed -i 's/hosts=.*/hosts=**ALL**/ vars/add_ansible_user.ini'
    sed -i 's/target_user=.*/target_user=**user**/ vars/add_ansible_user.ini'
    sed -i 's/user_to_create=.*/user_to_create=**ansible**/ vars/add_ansible_user.ini'
    sed -i 's/path_to_ssh_pub_key=.*/path_to_ssh_pub_key=**\/root\/\.ssh\/id_rsa\.pub\/**/' vars/add_ansible_user.ini
    ansible-playbook add_ansible_user.yaml 

----

## Notes
  Be sure to populate the vars/add_ansible_user.ini file with your variables.
  To maintain simplicity, this is really only meant to be run once. Though, it could easily be integrated into idempotent roles with some additional checks, such as the lineinfile to check for the user@server entry in the ssh key.
  There is an assumption that the remote_user has sudo privileges with the same ssh password.
