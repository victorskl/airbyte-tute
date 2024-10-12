# Kube

_observe kubernetes control plane set up by `abctl`_

```
docker ps -a | grep abctl-control-plane
e535c82d68ca   kindest/node:v1.29.8   "/usr/local/bin/entr…"   About an hour ago   Up About an hour   0.0.0.0:8000->80/tcp, 127.0.0.1:56114->6443/tcp   airbyte-abctl-control-plane
```

```
docker exec -it airbyte-abctl-control-plane bash
```

```
root@airbyte-abctl-control-plane:/# kubectl get pods --all-namespaces
NAMESPACE            NAME                                                      READY   STATUS      RESTARTS   AGE
airbyte-abctl        airbyte-abctl-airbyte-bootloader                          0/1     Completed   0          64m
airbyte-abctl        airbyte-abctl-connector-builder-server-6fc5c9c9fb-988w8   1/1     Running     0          62m
airbyte-abctl        airbyte-abctl-cron-6576bdd496-dwhtk                       1/1     Running     0          62m
airbyte-abctl        airbyte-abctl-pod-sweeper-pod-sweeper-7cbbf9cf6d-b4r2t    1/1     Running     0          62m
airbyte-abctl        airbyte-abctl-server-5f4f479686-mlzzh                     1/1     Running     0          62m
airbyte-abctl        airbyte-abctl-temporal-b6bc5996d-gwj4x                    1/1     Running     0          62m
airbyte-abctl        airbyte-abctl-webapp-67fdd44456-n8t56                     1/1     Running     0          62m
airbyte-abctl        airbyte-abctl-worker-7f84fc8c6f-xrcfz                     1/1     Running     0          62m
airbyte-abctl        airbyte-abctl-workload-api-server-797cf8994-v8v6n         1/1     Running     0          62m
airbyte-abctl        airbyte-abctl-workload-launcher-5fd5bc879f-dsphk          1/1     Running     0          62m
airbyte-abctl        airbyte-db-0                                              1/1     Running     0          64m
airbyte-abctl        airbyte-minio-0                                           1/1     Running     0          64m
ingress-nginx        ingress-nginx-controller-548874d566-fr969                 1/1     Running     0          52m
kube-system          coredns-76f75df574-6h8z4                                  1/1     Running     0          64m
kube-system          coredns-76f75df574-ncf5f                                  1/1     Running     0          64m
kube-system          etcd-airbyte-abctl-control-plane                          1/1     Running     0          64m
kube-system          kindnet-ttk49                                             1/1     Running     0          64m
kube-system          kube-apiserver-airbyte-abctl-control-plane                1/1     Running     0          64m
kube-system          kube-controller-manager-airbyte-abctl-control-plane       1/1     Running     0          64m
kube-system          kube-proxy-d79z2                                          1/1     Running     0          64m
kube-system          kube-scheduler-airbyte-abctl-control-plane                1/1     Running     0          64m
local-path-storage   local-path-provisioner-888b7757b-9hbcj                    1/1     Running     0          64m
```

```
root@airbyte-abctl-control-plane:/# kubectl get deployments --all-namespaces
NAMESPACE            NAME                                     READY   UP-TO-DATE   AVAILABLE   AGE
airbyte-abctl        airbyte-abctl-connector-builder-server   1/1     1            1           63m
airbyte-abctl        airbyte-abctl-cron                       1/1     1            1           63m
airbyte-abctl        airbyte-abctl-pod-sweeper-pod-sweeper    1/1     1            1           63m
airbyte-abctl        airbyte-abctl-server                     1/1     1            1           63m
airbyte-abctl        airbyte-abctl-temporal                   1/1     1            1           63m
airbyte-abctl        airbyte-abctl-webapp                     1/1     1            1           63m
airbyte-abctl        airbyte-abctl-worker                     1/1     1            1           63m
airbyte-abctl        airbyte-abctl-workload-api-server        1/1     1            1           63m
airbyte-abctl        airbyte-abctl-workload-launcher          1/1     1            1           63m
ingress-nginx        ingress-nginx-controller                 1/1     1            1           54m
kube-system          coredns                                  2/2     2            2           66m
local-path-storage   local-path-provisioner                   1/1     1            1           66m
```

```
root@airbyte-abctl-control-plane:/# kubectl get services --all-namespaces
NAMESPACE       NAME                                                 TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                        AGE
airbyte-abctl   airbyte-abctl-airbyte-connector-builder-server-svc   NodePort    10.96.182.170   <none>        80:31334/TCP                   63m
airbyte-abctl   airbyte-abctl-airbyte-server-svc                     ClusterIP   10.96.212.24    <none>        8001/TCP                       63m
airbyte-abctl   airbyte-abctl-airbyte-webapp-svc                     ClusterIP   10.96.8.211     <none>        80/TCP                         63m
airbyte-abctl   airbyte-abctl-temporal                               ClusterIP   10.96.170.168   <none>        7233/TCP                       63m
airbyte-abctl   airbyte-abctl-workload-api-server-svc                ClusterIP   10.96.77.23     <none>        8007/TCP                       63m
airbyte-abctl   airbyte-db-svc                                       ClusterIP   10.96.14.77     <none>        5432/TCP                       65m
airbyte-abctl   airbyte-minio-svc                                    ClusterIP   10.96.187.165   <none>        9000/TCP                       65m
default         kubernetes                                           ClusterIP   10.96.0.1       <none>        443/TCP                        66m
ingress-nginx   ingress-nginx-controller                             NodePort    10.96.68.162    <none>        8000:30773/TCP,443:31030/TCP   54m
ingress-nginx   ingress-nginx-controller-admission                   ClusterIP   10.96.222.48    <none>        443/TCP                        54m
kube-system     kube-dns                                             ClusterIP   10.96.0.10      <none>        53/UDP,53/TCP,9153/TCP         66m
```

```
root@airbyte-abctl-control-plane:/# kubectl get pv
NAME                CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                                                  STORAGECLASS   VOLUMEATTRIBUTESCLASS   REASON   AGE
airbyte-minio-pv    500Mi      RWO            Retain           Bound    airbyte-abctl/airbyte-minio-pv-claim-airbyte-minio-0   standard       <unset>                          67m
airbyte-volume-db   500Mi      RWO            Retain           Bound    airbyte-abctl/airbyte-volume-db-airbyte-db-0           standard       <unset>                          67m
```

```
root@airbyte-abctl-control-plane:/# kubectl get events --all-namespaces
<skip>
```

You got the idea! It becomes _KubeOps_.

Further deep dive:
- https://docs.airbyte.com/deploying-airbyte/
