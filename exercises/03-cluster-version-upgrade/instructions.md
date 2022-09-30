# Exercise 3

In this exercise, you will learn how to upgrade the cluster version from 1.22.0 to 1.23.4 using kubeadm. The cluster will contain of a single control plane node named `kube-control-plane`, and one worker node named `kube-worker-1`. The existing setup uses virtual machines (VMs) to emulate the cluster environment.

> **_NOTE:_** The file [vagrant-setup.md](../common/vagrant-setup.md) describes the setup instructions and commands for Vagrant and VirtualBox. If you do not want to use the Vagrant environment, you can use the Katacoda lab ["Upgrading a cluster version"](https://learning.oreilly.com/scenarios/cka-prep-upgrading/9781492095514/).

## Upgrading the Control Plane Node

1. Shell into the control plane node with `vagrant ssh kube-control-plane`.
2. Upgrade kubeadm to `1.23.4-00` via `apt-get`. Verify that the correct version has been set.
3. Drain the control plane node.
4. Use the appropriate kubeadm command to upgrade the control plane to `1.23.4`.
5. Uncordon the control plane node.
6. Upgrade kubelet and kubectl to `1.23.4-00`.
7. Restart the kubelet.
8. Exit out of the node.

## Upgrading the Worker Node

1. Shell into the worker node with `vagrant ssh kube-worker-1`.
2. Upgrade kubeadm to `1.23.4-00` via `apt-get`. Verify that the correct version has been set.
3. Drain the node.
4. Upgrade the kubelet configuration.
5. Upgrade kubelet and kubectl to `1.23.4-00`.
6. Restart the kubelet.
7. Uncordon the node.
8. Exit out of the node.

See notes in CKA google doc

A few things to memorise? The commands and the general process

Upgrade - upgrading subsquent control plane nodes is slightly different to upgrading the first one, see docs
Drain
Apply
Uncordon
Upgrade
Restart

Same for worker nodes

Attempt 2
- This is elementary
Could figure out a few things
- Why do daemonsets have to be ignored? What does daemon-reload accomplish?
- Do I have to ssh onto the nodes to upgrade them? I don't think so
- The specifics of what kubeadm, kubectl and kubelet do
- Why draining the nodes is necessary