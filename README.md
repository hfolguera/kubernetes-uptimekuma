# kubernetes-uptimekuma

## Requirements
UptimeKuma deployment is configured to use a MariaDB database as a repository. MariaDB deployment is required prior to continue with UptimeKuma deployment. Also, a dedicated database must exist.

[Deploy MariaDB](https://github.com/hfolguera/kubernetes-mariadb)

Execute the following commands to connect to the MariaDB instance:
```
POD=`kubectl get pod -n mariadb -o jsonpath='{.items[0].metadata.name}'`
kubectl exec -it -n mariadb $POD -- mariadb -u root -p
```

Then, create new databases and user:
```
create database uptimekuma;
create user 'uptimekuma'@'%' identified by '<PASSWORD>';
grant all privileges on uptimekuma.* to 'uptimekuma'@'%';


## Uptimekuma Deployment

```
kubectl apply -f uptimekuma-namespace.yaml
kubectl create secret generic uptimekuma-mariadb-pass -n uptimekuma --from-literal=username=uptimekuma --from-literal=password=<PASSWORD>
kubectl apply -f uptimekuma-pvc.yaml
kubectl apply -f uptimekuma-deployment.yaml
kubectl apply -f uptimekuma-service.yaml
```