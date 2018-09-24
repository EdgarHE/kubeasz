## image usage
## import VM
1. import 1 deploy VM and 2 worker VM, reinitialize MAC address, rename and chose cpu/memory wanted for them
2. boot the 3 VM and get their IPs with `ifconfig`

### Deploy cluster on the deploy VM
0. run every things as root
```bash
sudo su
```
1. setup ssh key
```bash
# generate ssh key
ssh-keygen -t rsa -b 2048
# (press Enter Enter Enter)

# setup no password access to all VMs (including deploy VM and Worker VM)
ssh-copy-id #all node IPs
# (yes and then type root password for target VM)
```
2. open ansible hosts file
```bash
# change IPs in hosts file
cd /etc/ansible
vim hosts
```
3. replace the right IPs in the following location with your deploy and worker IPs
```bash
# 集群部署节点：一般为运行ansible 脚本的节点
# 变量 NTP_ENABLED (=yes/no) 设置集群是否安装 chrony 时间同步
[deploy]
192.168.1.1 NTP_ENABLED=no

# etcd集群请提供如下NODE_NAME，请注意etcd集群必须是1,3,5,7...奇数个节点
[etcd]
192.168.1.1 NODE_NAME=etcd1

[kube-master]
192.168.1.1

[kube-node]
192.168.1.2
192.168.1.3
```
4. test connection to VMs
```bash
ansible all -m ping
```
5. deploy
```bash
ansible-playbook 90.setup.yml
```

