# redbee-challenge

# Iniciando minikube
minikube start

minikube addons enable ingress

# deployando volumenes

kubectl apply -f persistent-volume
kubectl apply -f persistent-volume-claim

# creamos un secret

podemos tomar 2 caminos o lo creamos por consola

kubectl create secret generic sql-password --from-literal=password=Password123

o deployamos el yaml

kubectl apply -f secrets

# Deployamos la base mysql con su servicio

kubectl apply -f mysql-deployment

# vemos el nombre del pod

kubectl get pods 

# Importamos la data

cd db

kubectl cp alta_db.sql <nombre del pod mysql>:alta_db.sql

kubectl exec <nombre del pod mysql> -- mysql -P3306 -h localhost -u root -pPassword123 < alta_db.sql

# Deployamos la api

kubectl apply -f api-deployment

# Deployamos el ingress

kubectl apply -f ingress

# Agregamos al archivo host nuestra dns

vi /etc/hosts

le agregamos:

192.168.49.2    redbee-challenge.com

Ahora podemos probar

curl http://redbee-challenge.com/quotes