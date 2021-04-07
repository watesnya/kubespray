# IT-Enterprise list
Install from haproxy machine

### 1) supo apt-get install git 
  Install a git to clone Repo

### 2) sudo mkdir /kube
  make directory to clone

### 3) sudo git clone https://github.com/Skatanic6996/kubespray

### 4) sudo nano /kube/kubespray/inventory/mycluster/hosts.yaml
  enter you names and IPs
  like:

``` js
all:
  hosts:
    my-best-master01:
      ansible_host: 192.168.0.1
      ip: 192.168.0.1
      acces_ip: 192.168.0.1
``` 
### 5) sudo nano /kube/kubespray/inventory/mycluster/group_vars/all/all.yml
  add your haproxy VIP like this :

loadbalancer_apiserver:
  address: 192.168.0.3
  port: 6443

### 6) Share your certs (from root)
ssh-keygen -t rsa
ssh-copy-id root@<your_node_ip>

try connect: ssh <your_node_ip>

### 7) Install requirements

sudo apt update 

sudo apt install software-properties-commosudo apt update 

sudo apt install python3.8 

sudo apt install python3-pip 

### 8) Go to main folder (cd /kube/kubespray)

### 9) Install cluster

ansible-playbook -i inventory/mycluster/hosts.yaml  --become --become-user=root cluster.yml --extra-vars "ansible_sudo_pass=<your_root_password>" --timeout 180




## Notes

If you need to install the cluster using http \ https proxy - you need to add these parameters before installation.

sudo nano inventory/mycluster/group_vars/all/all.yml

http_proxy: "192.168.0.1"
https_proxy: "192.168.0.1"
