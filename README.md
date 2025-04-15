# LSC-kube

First we need to install nfs server:
```
helm repo add nfs-ganesha-server-and-external-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner/
helm install my-release nfs-ganesha-server-and-external-provisioner/nfs-server-provisioner --set=storageClass.name=lsc
```

Next we can create claim on the pv using definition contained in `nfs.yaml` file
```
kubectl apply -f nfs.yaml
```

Then we polulate the drive with example data using jobs:
```
kubectl apply -f job.yaml
```

Lastly we need to create a pod with httpd server utilizing created claim:
```
kubectl apply -f http.yaml
```

To get the webside url we need to execute:
```
kubectl get service
```

Then we can copy the address under `EXTERNAL-IP` column and enjoy our webside!
