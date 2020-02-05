# Kubenetes Multi Node Cluster on Ubuntu Bionic

## Objective
Setup a full blown multi node kubenetes cluster on Ubuntu Bionic (18.04 LTS)

## Prerequisites
* Vagrant
* VirtualBox (or similar) as VM provider
* (Windows Only) guest_ansible vagrant plugin 

## Setup
### Checkout or download the code
```
git clone https://github.com/Chamindasl/kube-cluster.git
cd kube-cluster
```

### Spin up the cluster
```
vagrant up
``` 

### Verify
```
vagrant ssh km

vagrant@km:~$ kubectl get nodes -o wide
NAME   STATUS   ROLES    AGE   VERSION   INTERNAL-IP     EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
km     Ready    master   66m   v1.17.2   192.168.50.10   <none>        Ubuntu 18.04.4 LTS   4.15.0-76-generic   docker://19.3.5
kw1    Ready    <none>   35m   v1.17.2   192.168.50.20   <none>        Ubuntu 18.04.4 LTS   4.15.0-76-generic   docker://19.3.5
kw2    Ready    <none>   35m   v1.17.2   192.168.50.30   <none>        Ubuntu 18.04.4 LTS   4.15.0-76-generic   docker://19.3.5
```

## Disclaimer
This repo is based on original kubenetes post below. Its a great article. Thanks to Author: Naresh L J  
https://kubernetes.io/blog/2019/03/15/kubernetes-setup-using-ansible-and-vagrant/

### Why another
* Original is not working for Ubuntu Bionic (18.04 LTS), the latest ubuntu which has docker binaries. As of writing latest ubuntu server is Eoan Ermine, but no official docker binaries for Eoan Ermine yet.
* is not portable (not working for Windows)
* is not straight forward. have to compose together
* is not working for Kubenetes > 1.17.X
* not comes with Kubectul autocomplete 
    