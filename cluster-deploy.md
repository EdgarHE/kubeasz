## image usage
### on deploy VM
```bash
# setup no password access to all VMs (including deploy VM and Worker VM)
ssh-copy-id #all node IPs

# change IPs in hosts file
cd /etc/ansible
vim hosts

# test connection
ansible all -m ping

# deploy
ansible-playbook 90.setup.yml
```

