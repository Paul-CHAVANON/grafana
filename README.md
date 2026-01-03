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
```
sudo docker compose up -d
```
Lancer un docker compose du fichier docker-compose.yml <br/>
Source : [./grafana_prometheus_config/docker-compose.yml](https://github.com/Paul-CHAVANON/grafana/blob/main/grafana_prometheus_config/docker-compose.yml)

### Installer des exporter
Lancer les docker compose sur les VMs/Serveurs concernés
```
sudo docker compose up -d
```
Pour annalyser des données des VMs/serveurs
</br>- [./node_exporter/docker-compose.yml](https://github.com/Paul-CHAVANON/grafana/blob/main/node_exporter/docker-compose.yml)
</br></br>Pour annalyser des perfomance GPU Nvidia
</br>- [./nvidia_gpu_exporter/docker-compose.yml](https://github.com/Paul-CHAVANON/grafana/blob/main/nvidia_gpu_exporter/docker-compose.yml)


## Dashboard infrastructures
### Node Exporter full
Permet de connaitre les données de chaques node, réseaux, RAM, CPU, ... <br/>
Source : [Grafana-dashboard.com](https://grafana.com/grafana/dashboards/1860-node-exporter-full/)

### Nvidia Exporter
Source : [Grafana-dashboard.com](https://grafana.com/grafana/dashboards/14574-nvidia-gpu-metrics/)

## Dasboard applicatif
### Kubernetes cluster
Permet de connaitre les données du cluster Kube, RAM, Pods, ... <br/>
Source : [Grafana-dashboard.com](https://grafana.com/grafana/dashboards/15282-k8s-rke-cluster-monitoring/) compatible K8S + K3S

