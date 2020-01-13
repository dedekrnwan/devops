- Apply development elasticsearch: kubectl apply -f elasticsearch.yaml
- Setup security:
kubectl exec $(kubectl get pods -n development-monitoring | grep elasticsearch | sed -n 1p | awk '{print $1}') \
    -n development-monitoring \
    -- bin/elasticsearch-setup-passwords auto -b
save the result in file credentials.txt

- Save the credentials
    - Credentials for kibana
    kubectl create secret generic kibana-pw-elastic \
        -n development-monitoring \
        --from-literal password=jeNbRuuyhTdmBya81Zwg <-- cange this line with real pwd generated result
    - Credentials for apm_system
    kubectl create secret generic apm-pw-elastic \
        -n development-monitoring \
        --from-literal password=XWcWwq3u6eD2GbbNYsyw <-- cange this line with real pwd generated result
    - Credentials for beats_system
    kubectl create secret generic beats-pw-elastic \
        -n development-monitoring \
        --from-literal password=TXivbuKgUqOir5HfoEnL <-- cange this line with real pwd generated result

    - Credentials for elasticsearch
    kubectl create secret generic elasticsearch-pw-elastic \
        -n development-monitoring \
        --from-literal password=m7dQZcNcX9F5PlxEnbCx <-- cange this line with real pwd generated result
- Apply development kibana: kubectl apply -f kibana.yaml


-- kubernetes web ui dashboard
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta8/aio/deploy/recommended.yaml
