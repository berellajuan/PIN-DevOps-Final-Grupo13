# PIN-DevOps-Final-Grupo13
Trabajo practico Final DevOps MundosE

# Configurar Env de Jenikins
```sh
export KUBECONFIG=/var/jenkins_home/.kube/config
```
# EndPoint Nginx
- http://dev-env.grupo13.com/service/nginx

# ConfigMAP
```
kubectl delete configmaps prometheus-config
kubectl create configmap prometheus-config --from-file=prometheus.yml --namespace=monitoreo
```

## Node Explorer
```
node_cpu_seconds_total
node_memory_MemAvailable_bytes
```