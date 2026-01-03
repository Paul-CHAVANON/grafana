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

### Installer des exporter classic
Lancer les docker compose sur les VMs/Serveurs concernés
```
sudo docker compose up -d
```
Pour annalyser des données des VMs/serveurs
</br>- [./node_exporter/docker-compose.yml](https://github.com/Paul-CHAVANON/grafana/blob/main/node_exporter/docker-compose.yml)
</br></br>Pour annalyser des perfomance GPU Nvidia
</br>- [./nvidia_gpu_exporter/docker-compose.yml](https://github.com/Paul-CHAVANON/grafana/blob/main/nvidia_gpu_exporter/docker-compose.yml)

### Configurer l'export de metrics Kube
Récupérer le cetificat nécessaire sur le master node kube
```bash
sudo cat /var/lib/rancher/k3s/server/tls/server-ca.crt
```

Créer un ServiceAccount et un token
```
# 1. Créer le ServiceAccount
sudo kubectl create serviceaccount prometheus -n default --dry-run=client -o yaml | kubectl apply -f -

# 2. Créer un ClusterRoleBinding robuste
# Cela lie le ServiceAccount au rôle 'system:kubelet-api-admin' ou 'view'
sudo kubectl create clusterrolebinding prometheus-cluster-view \
  --clusterrole=cluster-admin \
  --serviceaccount=default:prometheus
# 3. Créer le token
sudo kubectl create token prometheus
```


Puis le configurer dans prometheus
```Docker-compose.yml
  - job_name: 'k3s-kubelet'
    scheme: https
    bearer_token: "<NODE-TOKEN-HERE>" # Récupéré de votre cluster
    tls_config:
ca_file: /etc/prometheus/ca.crt # Récupéré de votre cluster
insecure_skip_verify: true
    static_configs:
- targets: ['192.168.2.13:10250', '192.168.2.14:10250', '192.168.2.15:10250']
```

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

