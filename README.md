# Examples

This folder contains different examples of Strimzi custom resources and demonstrates how they can be used.

* [Kafka cluster](./kafka)
    * Kafka deployments with different types of storage
* [Kafka Connect and Kafka Connect Connector](./connect)
* [Kafka Mirror Maker 1 and 2](./mirror-maker)
* [Kafka Bridge](./bridge)
* [Cruise Control and Kafka Rebalance](./cruise-control)
* [Kafka users](./user)
* [Kafka topics](./topic)
* [Prometheus metric](./metrics)
    * Examples of Kafka components with enabled Prometheus metrics
    * Grafana dashboards
    * Prometheus Alert
    * Sample Prometheus installation files
    * Sample Grafana installation files
    * JMX Trans deployment
* [Security](./security)
    * Deployments of Kafka, Kafka Connect and HTTP Bridge using TLS encryption, authentication and authorization

-------------------------
Things I did:
* kubectl create ns kafka
* sed -i '' 's/namespace: .*/namespace: kafka/' install/cluster-operator/*RoleBinding*.yaml
* kubectl create ns my-kafka-project
* Edit the install/cluster-operator/060-Deployment-strimzi-cluster-operator.yaml file and set the STRIMZI_NAMESPACE environment variable to the namespace my-kafka-project
* kubectl create -f install/cluster-operator/ -n kafka
* kubectl create -f install/cluster-operator/020-RoleBinding-strimzi-cluster-operator.yaml -n my-kafka-project
* kubectl create -f install/cluster-operator/031-RoleBinding-strimzi-cluster-operator-entity-operator-delegation.yaml -n my-kafka-project
* kubectl create -n my-kafka-project -f examples/kafka/kafka-ephemeral-single.yaml
* kubectl create -n my-kafka-project -f examples/topic/kafka-topic.yaml
-------------------------
* akhq
  *  helm repo add akhq https://akhq.io/
  *  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=akhq,app.kubernetes.io/instance=akhq" -o jsonpath="{.items[0].metadata.name}")
  *  echo "Visit http://127.0.0.1:8080 to use your application"
  *  kubectl port-forward $POD_NAME 8080:80
-------------------------
* kubectl get svc -n my-kafka-project
* kubectl scale statefulset,deployment -n kafka --all --replicas=0
* kubectl scale statefulset,deployment -n my-kafka-project --all --replicas=0