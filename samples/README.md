# Test Vault Database Backend

## Install mysql server
```
$ helm install mysql-server stable/mysql
```
```
$ kubectl get service mysql-server
NAME           TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
mysql-server   ClusterIP   10.102.66.94   <none>        3306/TCP   5m38s
```
Get mysql root password:
```
$ MYSQL_ROOT_PASSWORD=$(kubectl get secret --namespace default mysql-server -o jsonpath="{.data.mysql-root-password}" | base64 --decode; echo)
```
