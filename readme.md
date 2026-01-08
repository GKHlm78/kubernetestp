# Mini-rapport Kubernetes - ServiceJava

## 1. Création du déploiement depuis une image Docker

### Commandes utilisées

```bash
# Vérification des nodes
kubectl get nodes

kubectl create deployment servicejava --image=battlcall/servicejava:latest

# Vérification des pods
kubectl get pods

# Entrée dans le pod en mode interactif
kubectl exec -it <nom_du_pod> -- /bin/bash
ls
exit
```

![Pod en mode interactif](screenshots\Screenshot 2026-01-08 163910.png)

## 2. Exposition du déploiement

### Commandes utilisées

```bash
kubectl expose deployment servicejava --type=NodePort --port=8080

kubectl get services

minikube service servicejava-nodeport --url
```
![Exposition](screenshots\Screenshot 2026-01-08 162528.png)

# 3. Scaling et load balancing

### Commandes utilisées

```bash
#Check si le service tourne:
kubectl get deployments

#Combien d'instance tourne actuellement:
kubectl get pods

#Lancer une deuxieme instance:
kubectl scale --replicas=2 deployment/servicejava
kubectl get deployments
```

![deuxieme pods](screenshots\Screenshot 2026-01-08 164044.png)

# 4. Créer un service de type LoadBalancer


### Commandes utilisées

```bash
kubectl expose deployment servicejava --type=LoadBalancer --port=8080

# Récupération de l'URL pour tester dans le navigateur
minikube service servicejava --url
```
![service load balancer running](screenshots\Screenshot 2026-01-08 164930.png)

# 5. Rolling updates

 ### Commandes utilisées

 ```bash
 kubectl set image deployments/my-deployment my-deployment=dockerHudId/my-image:v2
 ```
 ![set image](screenshots\Screenshot 2026-01-08 170547.png)

 ```bash
kubectl rollout undo deployments/my-deployment
```
[Undo](screenshots\Screenshot 2026-01-08 170719.png)
