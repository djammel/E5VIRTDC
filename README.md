# E5VIRTDC
Djamel MOAD Rendue 

# E5-CCISP
Djamel MOAD Rendue 




<!-- PROJECT LOGO --> <br /> <div align="center"> <h3 align="center">Projet Kubernetes : Applications e-commerce </h3> <p align="center"> 

<a href="https://github.com/app-generator/ecommerce-django-stripe"><strong>Documentation E-commerce django stripe</strong></a> <br /> 
<a href="https://docs.stripe.com/checkout/quickstart">Documentation Stripe premier pas</a> · 
<a href="https://github.com/app-generator/ecommerce-flask-stripe">Documentation Ecommerce Flask Stripe</a> · 


<!-- TABLE OF CONTENTS --> <details> <summary>Table des matières</summary> <ol> <li><a href="#structure-du-projet">Structure du projet</a></li> <li><a href="#configurations">Configurations</a></li> 
<li><a href="#etape-du-build">Étape du build</a></li> <li><a href="#logs">Logs</a></li> <li><a href="#quelques-interfaces">Quelques Interfaces</a></li> </ol> </details>



<!-- ABOUT THE PROJECT -->
## Struture du projet

Voici la structure du projet:

Composants Utilisés

Kubernetes

Pods : Conteneurisation des applications

Deployments : Gestion des versions et des mises à jour

Services : Exposition des applications sur le réseau

Ingress : Gestion du trafic sur les ports 80 et 443

ConfigMaps : Stockage des fichiers d'environnement non sensibles

Secrets : Stockage des informations sensibles (ex : clés API Stripe)

Namespaces : Isolation des environnements (Dev et Prod)

HPA (Horizontal Pod Autoscaler) : Scalabilité automatique selon la charge

Volumes persistants : Stockage des données sensibles de l'application

```bash
< PROJECT ROOT >
   |
   |-- apps/
   |    |-- django-soft-ui-dashboard/
   |    |-- flask-soft-ui-design/
   |    |-- ecommerce-flask-stripe/
   |    |-- rocket-django/
   |
   |-- nginx/
   |    |-- nginx.conf
   |
   |-- docker-compose.yml
   ************************************************************************
```


<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- FILES CONFIGURATIONS -->
## Configurations

. Contenu du compose.yaml

``` bash
version: '3.7'

services:
  django-soft-ui:
    # build: ./django-soft-ui-dashboard
    image: th0m8s/django-soft-ui-dashboard:prod
    ports:
"5080:5005"
networks:
app_network

  flask-soft-ui:
    # build: ./apps/flask-soft-ui-design
    image: th0m8s/flask-soft-ui-dashboard:prod
    ports: 
      
"5083:5008"
  networks:
app_network

  flask-material-dashboard:
    # build: ./apps/ecommerce-flask-stripe
    image: th0m8s/flask-material-dashboard:prod
    ports:
      
"5082:5007"
  networks:
app_network

  flask-atlantis-dark:
    # build: ./apps/rocket-django
    image: th0m8s/flask-atlantis-dark:prod
    ports:
"5081:5006"
networks:
app_network

  nginx:
    image: "nginx:mainline-alpine3.20-slim"
    ports:
"5080:5005"
"5081:5006"
"5082:5007"
"5083:5008"
volumes:
./nginx:/etc/nginx/conf.d
networks:
web_network
depends_on:
django-soft-ui
flask-soft-ui
flask-material-dashboard
flask-atlantis-dark

networks:
  app_network:
    driver: bridge
  web_network:
    driver: bridge

```

<!-- GETTING STARTED -->
## Etape du build

### Pour déployer les applications du répertoire "devoir":

Définition de l'architecture : Identification des composants et interactions

Configuration de Kubernetes : Mise en place des namespaces, deployments, services

Intégration de Stripe : Configuration de l'API avec secrets et configMaps

Gestion du scaling : Implémentation du HPA pour ajuster dynamiquement le nombre de pods

Tests de charge : Simulation de trafic et mesure des performances

Monitoring et Logging : Configuration de Prometheus et Grafana pour observer l'utilisation des ressources

Documentation et résultats : Explication des choix et analyse des performances

<!-- INTERFACES -->
## Quelques interfaces

Test de résilience : Détection des points de défaillance

Analyse des logs : Identification des anomalies et optimisation



. Test de paiement : Validation du bon fonctionnement des transactions Stripe

![alt text](screen/Dashboard.png)

. Soft UI Dashboard

![alt text](screen/SoftDashborad.png)

. Flask Materiaal Dashboard

![alt text](screen/flask.png)


## Choix des frameworks


Flask Soft UI Design

Léger et facile à utiliser.
Fournit une interface utilisateur moderne et personnalisable.

Ecommerce Flask Stripe

Simplifie l'intégration des paiements avec Stripe.
Idéal pour les projets de commerce électronique.

Rocket Django

Robuste et bien structuré pour des projets évolutifs.
Offre des fonctionnalités prédéfinies pour un développement rapide.
Ces frameworks sont légers, simples à prendre en main et proposent des exemples pratiques pour accélérer le développement tout en assurant une qualité professionnelle.

## Diagramme Projet

![alt text](screen/Schema3.png)
