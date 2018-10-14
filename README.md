# k8sFabricplayground

k8sFabricPlayground is based 
[k8sPlayground](https://github.com/redtree0/k8sPlayground) .

k8sFabricPlayground sets up a kubernetes cluster on three VirtualBox virtual machines (one master and two workers) running Ubuntu 18.04 LTS using [kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/).

### Change Log
* k8s specific version = 1.11.0
* docker specific version = docker-ce:17.03
* Switch a pod network, flannel
* increase master's memory 

### Prerequisites
* [Virtual environment](https://docs.python.org/3/library/venv.html) with Python3
* [Virtualbox](https://www.virtualbox.org/)

### Installation
```bash
$ git clone https://github.com/redtree0/k8sPlayground-HLF.git
$ cd k8sFabricPlayground
$ pip install virtualenv
$ virtualenv -p python3 k8s_env
$ source k8s_env/bin/activate
```
In the virtual environment, run

```
$ pip install -r requirements.txt
```
Install ansible roles.
```
$ ansible-galaxy install -r requirements.yml -p roles/
```

### Create Virtual Machines
Run `vagrant up` to bring up three virtual machines.

The hostnames and IP addresses of the machines are as follows:

kubemaster — 192.168.99.20

worker1 – 192.168.99.21

worker2 – 192.168.99.22

### Create kubernetes cluster
```
$ make cluster
```
As soon as it is done, you can ssh into kubemaster to see the nodes in the cluster by running `kubectl get nodes`. They may take a while to get ready. You should see something like this:
```
NAME         STATUS    ROLES     AGE       VERSION
kubemaster   Ready     master    6m        v1.10.3
worker1      Ready     <none>    5m        v1.10.3
worker2      Ready     <none>    5m        v1.10.3
```

### Tear down cluster
```
$ make clean
```
This will drain the nodes, make sure that they are empty before shutting them down and reset all kubeadm installed state.
