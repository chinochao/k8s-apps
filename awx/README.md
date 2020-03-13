# AWX K8s Deployment

# Pre Deployment
Create Secrets named:
awx-psgl with username and password
awx-secrets with username and password

Create Certificate for your Load Balance

## Deployment
Deploy in order:

**0-awx-configmaps.yaml**: deploys configmaps used in Nginx config, AWX settings.py, and AWX SECRET_KEY.
**UPDATE THE SECRET_KEY**
```
kubectl apply -f 0-awx-configmaps.yaml
```

**1-awx-rabbit.yaml**: deploys RabbitMQ pod and service.
```
kubectl apply -f 1-awx-rabbit.yaml
```

**2-awx-memcached.yaml**: deploys Memcached pod and service.
```
kubectl apply -f 2-awx-memcached.yaml
```

**3-awx-postgres.yaml**: deployes PVC, PostgreSQL pod, and service.
```
kubectl apply -f 3-awx-postgres.yaml
```

**4-awx-customenvs.yaml**: deploys a CentOS pod used to install custom virtualenvs and place them in PVC
```
kubectl apply -f 4-awx-customenvs.yaml
```

**5-awx-task.yaml**: deploys AWX Tasks DaemonSet.
```
kubectl apply -f 5-awx-task.yaml
```

**6-awx-web.yaml**: deploys AWX Web DaemonSet, service, and ingress. 
```
kubectl apply -f 6-awx-web.yaml
```