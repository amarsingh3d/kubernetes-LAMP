#How to Setup Lamp Stack on Kubernetes Cluser

Let's follow the steps below to create LAMP stack on Kubernetes Cluser

**Step-1: Clone Git repository:**

We need to clone git repository, in order to download Apache,PHP,MySQL and PhpMyAdmin yaml file.

To clone git repository run the following command.
```
$ git clone https://github.com/amarsingh3d/kubernetes-LAMP.git
```
Clone output would be like this
```
Cloning into 'kubernetes-LAMP'...
remote: Enumerating objects: 12, done.
remote: Counting objects: 100% (12/12), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 12 (delta 2), reused 12 (delta 2), pack-reused 0
Unpacking objects: 100% (12/12), done.
```

Once download finish, change directory

```
$ cd cd kubernetes-LAMP/
```

**Step-2: Create Apache,PHP,MySQL,PhpMyAdmin Deployment & Service**

Run command below to create Apache & PHP deployment and Service

```
$ kubectl create -f Apache_PHP_App.yaml

deployment.extensions/phpdeployment created
service/phpservice created
```
To Create MySQL Deployment and Service run following Command.

```
$ kubectl create -f mysql.yaml

deployment.extensions/mysqldeploy created
service/mysql-service created
```
Create PhpMyAdmin pod and service.

```
$ kubectl create -f phpmyadmin.yaml


service/phpmyadmin created
pod/phpmyadmin created
```

**Step-3: Validate created Service and pods**

To check service run following command

```
$ kubectl get svc

**NAME**            **TYPE**           **CLUSTER-IP**       **EXTERNAL-IP**                                                               **PORT(S)**          **AGE**
  kubernetes         ClusterIP         10.100.0.1             <none>                                                                        443/TCP              12d
  mysql-service      NodePort          10.100.133.204         <none>                                                                        3306:30006/TCP       4m
  phpmyadmin         LoadBalancer      10.100.124.42          a923b8ce414c611e9a4580e9bc01181a-1306726413.us-east-1.elb.amazonaws.com       80:31136/TCP         4m
  phpservice         LoadBalancer      10.100.252.156         a145801e314c711e9878e0a7065e7328-1743249526.us-east-1.elb.amazonaws.com       80:30080/TCP         25s
```

**Check running pods**

```
$ kubectl get pods -o=wide
**NAME**                             **READY**     **STATUS**    **RESTARTS**   **AGE**       **IP**                **NODE**                              **NOMINATED NODE**
  mysqldeploy-5c9dcc8c55-bhqrj         1/1           Running        0             15m       192.168.183.108   ip-192-168-170-141.ec2.internal               <none>
  phpdeployment-7fc9485dbf-82tpn       1/1           Running        0             12m       192.168.86.181    ip-192-168-106-201.ec2.internal   			<none>
  phpmyadmin                           1/1           Running        0             15m       192.168.167.172   ip-192-168-170-141.ec2.internal   			<none>
```

**Test Apache, PHP and PhpMyAdmin access**

Open browser and open phpservice external IP url:

http://a145801e314c711e9878e0a7065e7328-1743249526.us-east-1.elb.amazonaws.com/

Check PHPInfo

http://a145801e314c711e9878e0a7065e7328-1743249526.us-east-1.elb.amazonaws.com/phpinfo.php

Test PhpMyAdmin login

http://a923b8ce414c611e9a4580e9bc01181a-1306726413.us-east-1.elb.amazonaws.com/

User: **root**

Password: **redhat**    // We setup MySQL root password in our Mysql.yaml deployment file.//


