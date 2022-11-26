# k8s-lab

Generate full featured K8S labs using libvirt.

# Features

- HA 3-master deployments on a dedicated private subnet
- Uses [kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/) for a vanilla Kubernetes install
- [kube-vip](https://kube-vip.io/) for the HA control plane and `LoadBalancer` IPs
- [flannel](https://github.com/flannel-io/flannel) for a simple VXLAN pod network

# Usage

Set your inventory for the # of masters / workers you like. It's been tested with 3 masters, and 3 workers.

- `ansible-playbook -i inventory provision.yml` (this will modify your inventory file)
- `ansible-playbook -i inventory cluster.yml` (creates a usable cluster)

# Result

```
root@master1:~# kubectl get nodes -o wide
NAME      STATUS   ROLES           AGE     VERSION   INTERNAL-IP       EXTERNAL-IP   OS-IMAGE                         KERNEL-VERSION    CONTAINER-RUNTIME
master1   Ready    control-plane   6m2s    v1.25.4   192.168.123.139   <none>        Debian GNU/Linux 11 (bullseye)   5.10.0-19-amd64   cri-o://1.23.4
master2   Ready    control-plane   4m36s   v1.25.4   192.168.123.169   <none>        Debian GNU/Linux 11 (bullseye)   5.10.0-19-amd64   cri-o://1.23.4
master3   Ready    control-plane   3m41s   v1.25.4   192.168.123.211   <none>        Debian GNU/Linux 11 (bullseye)   5.10.0-19-amd64   cri-o://1.23.4
worker1   Ready    <none>          3m5s    v1.25.4   192.168.123.153   <none>        Debian GNU/Linux 11 (bullseye)   5.10.0-19-amd64   cri-o://1.23.4
worker2   Ready    <none>          3m5s    v1.25.4   192.168.123.190   <none>        Debian GNU/Linux 11 (bullseye)   5.10.0-19-amd64   cri-o://1.23.4
worker3   Ready    <none>          3m5s    v1.25.4   192.168.123.179   <none>        Debian GNU/Linux 11 (bullseye)   5.10.0-19-amd64   cri-o://1.23.4
root@master1:~#
```

# Bugs

- cURLing an nginx LB from the host takes wayyyy to long to return

# TODO

- Make everything more customizable through Ansible
