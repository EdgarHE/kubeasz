## image usage
## import VM
1. import 1 deploy VM and 2 worker VM, rename and chose cpu/memory wanted for them
2. chose the right Netowrk device and refresh MAC address in VM `Settings/Network`
3. boot the 3 VM and get their IPs with `ifconfig`

### Deploy cluster on the deploy VM
```bash
# run as root user
sudo su

# generate ssh key
ssh-keygen -t rsa -b 2048
# (press Enter Enter Enter)

# setup no password access to all VMs (including deploy VM and Worker VM)
ssh-copy-id #all node IPs
# (press Enter and then root password: 123456)

# change IPs in hosts file
cd /etc/ansible
vim hosts

# test connection
ansible all -m ping

# deploy
ansible-playbook 90.setup.yml
```

