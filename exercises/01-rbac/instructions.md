# Exercise 1

In this exercise, you will define Role Based Access Control (RBAC) to grant permissions to a specific user. The permissions should only apply to certain API resources and operations.

The following image shows the high-level architecture.

![rbac](imgs/rbac.png)

> **_NOTE:_** If you do not already have a cluster, you can create one by using minikube or you can use the Katacoda lab ["Setting up RBAC for a user"](https://learning.oreilly.com/scenarios/cka-prep-setting/9781492095477/).

## Creating the Client Certificate

Run the following commands will create the key and certificate sign request (CSR) needed for the user on Minikube. The user will be called `johndoe`. For detailed information, see this [blog post](https://www.adaltas.com/en/2019/08/07/users-rbac-kubernetes/#users-creation-and-authentication-with-x509-client-certificates). You can assume that you do not have to memorize these instructions for the exam.

What are the three things that are needed and why? key, csr and cert?

```
$ mkdir cert && cd cert
$ openssl genrsa -out johndoe.key 2048
Generating RSA private key, 2048 bit long modulus
...................................+++
...........................+++
$ openssl req -new -key johndoe.key -out johndoe.csr -subj "/CN=johndoe/O=group1"
$ openssl x509 -req -in johndoe.csr -CA ~/.minikube/ca.crt -CAkey ~/.minikube/ca.key -CAcreateserial -out johndoe.crt -days 500
Signature ok
subject=/CN=johndoe/O=group1
Getting CA Private Key
```

Creating a user is about kubeconfig, not the cluster itself. It is a matter of how you connect with it, rather than being an object you create in the cluster

Nonetheless, authenticated users still need authorisation - they need roles and role bindings, or cluster roles and cluster role bindings

kubectl config merely modifies the kube/config file

## Creating the User

1. Set the user entry in `kubeconfig`.
2. Set a context entry in `kubeconfig` named `johndoe`. Verify its existence.
3. Change the context to `johndoe`. Create a new Pod. What would you expect to happen?

## Granting Access to the User

1. Switch back to the original context.
2. Create a new Role named `pod-reader`. The Role should grant permissions to get, watch and list Pods.
3. Create a new RoleBinding named `read-pods`. Map the user `johndoe` to the Role named `pod-reader`.
4. Make sure that both objects have been created properly.
5. Switch to the context named `johndoe-context`.
6. Create a new Pod named `nginx` with the image `nginx`. What would you expect to happen?
7. List the Pods in the namespace. What would you expect to happen?

My overview of steps:
- Authentication is mediated by kube config. We can use certificates or gcloud accounts
- Authenticated users still need authorisation. This means roles and role bindings (or their cluster equivalent)