# k8s-pinger
This is Helm-chart for Kubernetes Nodes pinger, which created by Flant. 
(ref: https://medium.com/flant-com/ping-monitoring-between-kubernetes-nodes-11e815f4eff1)
##
Steps for install pinger: 

```bash
helm repo add pinger https://madenginex.github.io/k8s-pinger/

helm repo update

helm upgrade --install k8s-pinger pinger/k8s-pinger -f .\k8s-pinger\values.yaml -n monitoring ##or other namespace 
```



To make sure the installation was successful, go to any Node in the `/var/run/node-exporter-textfile` directory
there you should see the metrics in a text file.


##
In order for these metrics to get into Prometheus in the future, you need to set up NodeExporter.
In my case (i use helm/kube-prometheus-stack) i've added this lane in values.yaml 

```
prometheus-node-exporter:
  extraArgs:
    - --collector.textfile.directory=/host/textfile
  extraHostVolumeMounts: 
    - name: textfile
      hostPath: /var/run/node-exporter-textfile
      mountPath: /host/textfile
      readOnly: true
```

##
Dashboard
![dashboard](https://github.com/MadEngineX/k8s-pinger/blob/main/docs/sda.png)

Dasboard JSON: https://github.com/MadEngineX/k8s-pinger/blob/main/docs/dashboard.json
