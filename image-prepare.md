
## All server
 ```bash
# 文档中脚本默认均以root用户执行
apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y
# 安装python2
apt-get install python2.7
# Ubuntu16.04可能需要配置以下软连接
ln -s /usr/bin/python2.7 /usr/bin/python
 ```

 ```bash
 sudo passwd root
 sudo vi /etc/ssh/sshd_config
 #PermitRootLogin prohibit-password
PermitRootLogin yes
 # Start ssh service
service ssh start
 ```

 ## Deply server

 ```bash
apt-get install git python-pip -y
pip install pip --upgrade
```
`vim /usr/bin/pip`
```python
#原代码
from pip import main
if __name__ == '__main__':
    sys.exit(main())

#修改后
from pip import __main__
if __name__ == '__main__':
    sys.exit(__main__._main())
```
```bash
pip install ansible
git clone https://github.com/gjmzj/kubeasz.git
mkdir -p /etc/ansible
mv kubeasz/* /etc/ansible
cd /etc/ansible && cp example/hosts.s-masters.example hosts

ssh-keygen -t rsa -b 2048 回车 回车 回车
ssh-copy-id 192.168.3.59
ssh-copy-id 192.168.3.60
ssh-copy-id 192.168.3.61
```
