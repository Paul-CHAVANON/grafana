# Projet soumis à licence
Voir fichier LICENSE

# Grafana
## Présentation
Ce repository est composé en 3 parties
- "**_Configuration fonctionelle de Grafana et prometheus_**" Explication fonctionelle de grafana et prometheus

- "**_Dashboard infrastrucure_**" monitoring de serveurs et infrastructures

- "**_Dasboard applicatif_**" monitoring d'application comme Kubernetes


## Configuration fonctionelle de Grafana et prometheus
### Installer Docker 
Source : https://docs.docker.com/engine/install/ubuntu/

### Installer Grafana et Prometheus
Lancer un docker compose du fichier docker-compose.yml <br/>
Source : ./grafana_prometheus_config/docker-compose.yml

### Installer des exporter
Lancer les docker compose sur les VMs/Serveurs concernés
```
sudo docker compose up -d
```
Pour annalyser des perfomance GPU Nvidia
</br>- ./nvidia_gpu_exporter/docker-compose.yml
</br>Pour annalyser des données des VMs/serveurs
</br>- ./node_exporter/docker-compose.yml
</br>Pour annlayser des données Kubernetes
</br>- ./kube_exporter/docker-compose.yml


## Dashboard infrastructures


## Dasboard applicatif
