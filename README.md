# airbyte-tute

- https://github.com/airbytehq/airbyte
- https://docs.airbyte.com/using-airbyte/getting-started/oss-quickstart

> Heads-up: You should have a good decent resourceful (CPU/RAM) workstation or VM instance to try this tute. 

```
brew tap airbytehq/tap
brew install abctl
```

```
abctl local install --host localhost
  INFO    Thanks for using Airbyte!
          Anonymous usage reporting is currently enabled. For more information, please see https://docs.airbyte.com/telemetry
  INFO    Using Kubernetes provider:
            Provider: kind
            Kubeconfig: ~/.airbyte/abctl/abctl.kubeconfig
            Context: kind-airbyte-abctl
 SUCCESS  Found Docker installation: version 27.2.0
  INFO    No existing cluster found, cluster 'airbyte-abctl' will be created
 SUCCESS  Port 8000 appears to be available
 SUCCESS  Cluster 'airbyte-abctl' created
  INFO    Namespace 'airbyte-abctl' created
  INFO    Persistent volume 'airbyte-minio-pv' created
  INFO    Persistent volume 'airbyte-volume-db' created
  INFO    Persistent volume claim 'airbyte-minio-pv-claim-airbyte-minio-0' created
  INFO    Persistent volume claim 'airbyte-volume-db-airbyte-db-0' created
  INFO    Starting Helm Chart installation of 'airbyte/airbyte' (version: 1.1.0)
 SUCCESS  Installed Helm Chart airbyte/airbyte:
            Name: airbyte-abctl
            Namespace: airbyte-abctl
            Version: 1.1.0
            AppVersion: 1.1.0
            Release: 1
  INFO    Starting Helm Chart installation of 'nginx/ingress-nginx' (version: 4.11.3)
 SUCCESS  Installed Helm Chart nginx/ingress-nginx:
            Name: ingress-nginx
            Namespace: ingress-nginx
            Version: 4.11.3
            AppVersion: 1.11.3
            Release: 1
  INFO    No existing Ingress found, creating one
 SUCCESS  Ingress created
 SUCCESS  Launched web-browser successfully for http://localhost:8000
 SUCCESS  Airbyte installation complete.
            A password may be required to login. The password can by found by running
            the command abctl local credentials
```

```
abctl local credentials --email user@company.example
```

### Set up a Connection

- https://docs.airbyte.com/using-airbyte/core-concepts/
- https://docs.airbyte.com/using-airbyte/getting-started/add-a-source
- https://docs.airbyte.com/using-airbyte/getting-started/add-a-destination
- https://docs.airbyte.com/using-airbyte/getting-started/set-up-a-connection

```
- Connections > New Connection 
- Define Source > Set up a new source > Marketplace > at Search box: "Sample Data (Faker)"
- Define destination > Set up a new destination > Marketplace > at Search box: "Local JSON" > at Destination Path: `/tmp/airbyte_local`
```

### Clean up

```
abctl local uninstall --persisted
```

```
rm -rf ~/.airbyte/abctl
```

```
brew uninstall abctl
brew untap airbytehq/tap
```
