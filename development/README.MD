ref: https://kauri.io/article/b3be4dbf895b433f93b3cb589d414988
- Apply development namespace: kubectl apply -f namespace.yaml
- Apply development es-master kubectl apply -f es-master.yaml
- Apply development es-data: kubectl apply -f es-data.yaml
- Apply development es-client: kubectl apply -f es-client.yaml
- Setup security:
kubectl exec $(kubectl get pods -n staging-monitoring | grep elasticsearch-client | sed -n 1p | awk '{print $1}') \
    -n staging-monitoring \
    -- bin/elasticsearch-setup-passwords auto -b
save the result in file credentials.txt
- Save the credentials
kubectl create secret generic elasticsearch-pw-elastic \
    -n staging-monitoring \
    --from-literal password=NNBdF1DS9CIKpBnuRP2T <-- cange this line with real pwd generated result
- Apply development kibana: kubectl apply -f kibana.yaml
- Apply development apm-server: kubectl apply -f apm-server.yaml (akses: http://apm-server.staging-monitoring.svc.cluster.local:8200)
- Apply development filebeat: kubectl apply -f filebeat.yaml
- Apply development metricbeat: kubectl apply -f metricbeat.yaml
- Apply development es-curator: kubectl apply -f es-curator.yaml
- Apply ssl ssl/staging-* or ssl/production-*: kubectl apply -f ssl/comodo-staging.
- Expose kibana using nginx-ingress (using cd ingress/helm-chart, helm install --generate-name .)
ref: https://github.com/nginxinc/kubernetes-ingress/tree/master/deployments/helm-chart
- Test kibana: admin:gotebengan123
