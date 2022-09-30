# Exercise 4

In this exercise, you will identify the configuration of the etcd database, back it up and restore the original database from a backup file. The command line tool `etcdctl` has already been pre-installed on the control plane node.

> **_NOTE:_** The file [vagrant-setup.md](../common/vagrant-setup.md) describes the setup instructions and commands for Vagrant and VirtualBox. If you do not want to use the Vagrant environment, you can use the Katacoda lab ["Backing up and restoring etcd"](https://learning.oreilly.com/scenarios/cka-prep-backing/9781492095521/).

1. Shell into control plane node using the command `vagrant ssh kube-control-plane`.
2. Check that all nodes have been correctly registered and are in the "Ready" status.
3. Find out the version of etcd running in the cluster.
4. Identify the endpoint URL for the etcd service, the location of the server certificate and the location of the CA certificate.
5. Create a snapshot of the etcd database. Store the backup in the file `/opt/etcd-backup.db`.
6. Restore the original state of the cluster from the backup file at `/opt/etcd-backup.db` to the directory `/var/lib/from-backup`.
7. Point etcd to the new directory containing the restored backup. Restart the etcd Pod.

A few steps to understand and practice. A few filepaths to memorise

Etcd is a pod in kube-system
Presume it writes to the node file system, so accessing it for cert info is equivalent to sshing onto node
Snapshot itself has to be doe via the node?

2nd attempt
Difficult. I don't understand what is going on. Messy as I wasn't focussing
Need to find the etc d pod. This is likely to be in kube-system namespace
Where does the endpoint come from? It is also in the etcd pod descrition --listen-client-urls, but it is not needed, as we are on the control plane node already
The etcd backup command needs to be directed to 3 distinct files
We use the pod volume hostpaths to find where on the control plane etcd certs etc are stored
Carry out the copy command
Leave it there for safe keeping
To restore, use the restore command. I overlooked this
Then, manually change the path on the pod for etcd-data 
Backup the existing file before restoring it