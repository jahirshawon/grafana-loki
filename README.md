The following are the prerequisites for this setup.

1. Kubernetes Cluster
2. Helm installed in your system

If you are ready with the prerequisites, follow the steps below to set up Grafana Loki Logging on Kubernetes using Helm.

*Add Grafana repo to your system to download the helm chart to set up Grafana Loki Logging. Run the following command to add the repo

$ helm repo add grafana https://grafana.github.io/helm-charts

*Once the repo is added, run the following command to update the repo to make sure the repo is up-to-date.

$ helm repo update

*Now, list every repo with the word Loki using the command

$ helm search repo loki

*Use the below command to save the default values of the helm chart in a YAML file.

$ helm show values grafana/loki-stack > loki.yaml

*Now, in the loki.yaml, make changes to the Grafana configuration block because it is set to false by default, change grafana image version, expose grafana service to nodeport and changes are updated in loki.yaml.

Deploy grafana loki Now !! 
*Once the values are changed deploy the Loki Helm chart with the YAML file using the following command

$ helm upgrade --install --values loki.yaml loki grafana/loki-stack -n grafana-loki --create-namespace

This creates a namespace grafana-loki and deploys every component for the Grafana Loki Logging on Kubernetes.

*verify everything has deployed and running properly using the command

$ kubectl get pod -n grafana-loki

Access your Grafana on the browser by searching as localhost:nodeport
Login to Grafana using the username and password. Your default username will be admin and to get the password run the following command.

$ kubectl get secret --namespace grafana-loki loki-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
![2024-06-09_00-17](https://github.com/jahirshawon/grafana-loki/assets/56890366/1059925f-9af0-4173-8f8d-0829cd2c392c)

This command will show your password for Grafana, use the password and login to Grafana.
![Screenshot from 2024-06-09 00-05-30](https://github.com/jahirshawon/grafana-loki/assets/56890366/2cfbb0d6-2f18-4948-9b84-abaca1dbc8ee)

To query logs select a Label and Value, Loki will collect every log in your Kubernetes cluster and label it according to container, pod, namespace, and other Kubernetes objects.
![2024-06-09_00-12](https://github.com/jahirshawon/grafana-loki/assets/56890366/dc99e4d6-5b44-4337-98db-be4196d34bd1)







