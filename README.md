# Keptn Monday.com Notification Service
This service creates tickets on [Monday.com](https://monday.com) boards when a keptn evaluation (`sh.keptn.event.start-evaluation`) is performed. The service subscribes to the following keptn events:

* `sh.keptn.events.evaluation-done`

# Install Monday.com Notification Service into Keptn Cluster
1. Clone this repo onto the keptn machine.
1. Adjust the `monday-api-key`, `board-id` and `group-name` values in `monday-config-map.yaml` to reflect your values.
1. Use kubectl to apply the files `monday-config-map.yaml`, `monday-service.yaml` and `monday-distributor.yaml` files on the keptn cluster:

```
cd ~/keptn-monday-service
kubectl apply -f monday-config-map.yaml -f monday-service.yaml -f monday-distributor.yaml
```

Expected output:
```
configmap/monday-config-map created
deployment.apps/monday-service created
service/monday-service created
deployment.apps/monday-service-deployment-distributor created
```

# Verification of Installation
```
kubectl -n keptn get pods | grep monday
```

Expected output:
```
monday-service-*-*                                 1/1     Running   0          45s
monday-service-deployment-distributor-*-*          1/1     Running   0          45s
```

Now start an evaluation and wait for the ticket to be created. Note: You must have your services tagged with `keptn_project`, `keptn_service` and `keptn_stage`.
```
keptn send event start-evaluation --project=*** --stage=*** --service=*** --timeframe=2m
```
