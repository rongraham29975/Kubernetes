# Kubernetes
Mac shell and yaml files to automate kubernetes Couchbase cluster

https://blog.couchbase.com/couchbase-autonomous-operator-proof-of-concept-guide/

Brew install kind

Create yaml file
kind create cluster --name=couchbase --config=kind-config.yaml

PATH = /usr/local/Cellar/kind/0.11.1/bin

kind create cluster --name=couchbase --config=kind-config.yaml

 kubectl cluster-info --context kind-couchbase
—context - interact with different clusters

 k config get-contexts
CURRENT   NAME             CLUSTER          AUTHINFO         NAMESPACE
          docker-desktop   docker-desktop   docker-desktop   
*         kind-couchbase   kind-couchbase   kind-couchbase   
          minikube         minikube         minikube         default

Installing CB AO on Kubernetes cluster
Download and unzip
K create -f crd.yaml
(Customer resource definition)

DAC - dynamic Admission Controller
 bin/cbopcfg create admission

Install the operator
$ bin/cbopcfg create operator

Verifying…
k get deployments
NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
couchbase-operator             1/1     1            1           2m15s
couchbase-operator-admission   1/1     1            1           3m37s

Modify yaml file
K replace -f data_cluster.yaml

K get pods

k get pods -l couchbase_cluster=cb-example,couchbase_service_data=enabled
NAME              READY   STATUS    RESTARTS   AGE
cb-example-0000   1/1     Running   0          6m
cb-example-0001   1/1     Running   0          5m8s
cb-example-0002   1/1     Running   0          4m8s

kubectl get deployments

bin/cbopcfg delete operator
$ bin/cbopcfg delete admission
$ kubectl delete -f crd.yaml

Secrets
k get secrets
k delete secrets cb-example
===========================Grafana-Prometheus
Install brew
brew install kubernetes-service-catalog-client
Brew install kind
Download and unzip CAO 2.2.1
Download and unzip Service catalog 

docker run --name couchbase-exporter -d -p 9091:9091 couchbase-exporter:1.0.0
mcluster.sh
helm upgrade --install --set clusterName=scale-couchbase-cluster monitor couchbase/couchbase-monitor-stack 
kubectl port-forward service/grafana 3000:3000 
 kubectl port-forward --namespace default prometheus-couchbase-monitor-stack-prometheus-0 9090:9090
 kubectl port-forward cb662-0000 8091 &Handling connection for 8091


Install service catalog
https://issues.couchbase.com/browse/SBEE-26
helm repo add svc-cat https://kubernetes-sigs.github.io/service-catalog
helm install catalog svc-cat/catalog
brew install kubernetes-service-catalog-client
kubectl create -f ./crd.yaml # install 2.2.0 crd
Kubectl get pods
kubectl create -f /Users/rongraham/Documents/kubernetes/couchbase-service-broker-kubernetes/crd.yaml #Service Broker
kubectl create -f /Users/rongraham/Documents/kubernetes/couchbase-service-broker-kubernetes/demo-clusterservicebroker.yaml
kubectl create -f /Users/rongraham/Documents/kubernetes/couchbase-service-broker-kubernetes/demo-servicebroker.yaml
./cbsbctl.darwin create clusterservicebroker --profile=demo
kubectl get pods
kubectl get clusterservicebrokers
svcat get class
svcat get plans
svcat provision csb --class cao-2.2-service --plan csb-basic --param password=password --wait

Monitoring
   # Couchbase
   kubectl port-forward  cb662-0000 8092:8091
   #open localhost:8092

   # Prometheus
   kubectl port-forward --namespace default prometheus-couchbase-monitor-stack-prometheus-0 9090:9090
   # open localhost:9090

   # Grafana
   kubectl port-forward --namespace default deployment/monitor-grafana 3000:3000
   # open localhost:3000
   # login admin:admin

   # Couchbase service broker
   kubectl port-forward  couchbase-instance-24vw7jer-0000 8091:8091
   #open localhost:8092


k get pods --all-namespaces

kubectl port-forward --namespace default prometheus-couchbase-monitor-stack-prometheus-0 9090:9090

docker run   -p 9090:9090   -v /Users/rongraham/Documents/kubernetes/prometheus.yaml:/etc/prometheus/prometheus.yaml   prom/prometheus

IP address
k get pods -o wide
