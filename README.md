cat <<EOF | kubectl apply -f -
apiVersion: kafka.strimzi.io/v1beta1
kind: KafkaTopic
metadata:
  name: my-topic
spec:
  partitions: 1
  replicas: 1
  config:
    retention.ms: 7200000
    segment.bytes: 1073741824
EOF
Error from server ([denied by strimzi-cluster-label] you must provide labels: {"strimzi.io/cluster"}): error when creating "STDIN": admission webhook "validation.gatekeeper.sh" denied the request: [denied by strimzi-cluster-label] you must provide labels: {"strimzi.io/cluster"}





cat <<EOF | kubectl apply -f -
apiVersion: kafka.strimzi.io/v1beta1
kind: KafkaTopic
metadata:
  name: my-topic
  labels:
    strimzi.io/cluster: my-cluster
spec:
  partitions: 1
  replicas: 1
  config:
    retention.ms: 7200000
    segment.bytes: 1073741824
EOF
Error from server ([denied by strimzi-replicas] Topic must have at least 3 replicas and 2 min.insync.replicas): error when creating "STDIN": admission webhook "validation.gatekeeper.sh" denied the request: [denied by strimzi-replicas] Topic must have at least 3 replicas and 2 min.insync.replicas









cat <<EOF | kubectl apply -f -
apiVersion: kafka.strimzi.io/v1beta1
kind: KafkaTopic
metadata:
  name: my-topic
  labels:
    strimzi.io/cluster: my-cluster
spec:
  partitions: 1
  replicas: 3
  config:
    retention.ms: 7200000
    segment.bytes: 1073741824
    min.insync.replicas: 2
EOF
kafkatopic.kafka.strimzi.io/my-topic created








cat <<EOF | kubectl apply -f -
apiVersion: kafka.strimzi.io/v1beta1
kind: KafkaUser
metadata:
  name: my-user
  labels:
    strimzi.io/cluster: my-cluster
spec:
  authentication:
    type: tls
EOF
Error from server ([denied by strimzi-labels] strimzi.io/cluster label must contain one of the existing clusters): error when creating "STDIN": admission webhook "validation.gatekeeper.sh" denied the request: [denied by strimzi-labels] strimzi.io/cluster label must contain one of the existing clusters





cat <<EOF | kubectl apply -f -
apiVersion: kafka.strimzi.io/v1beta1
kind: KafkaUser
metadata:
  name: my-user
  labels:
    strimzi.io/cluster: my-cluster
spec:
  authentication:
    type: tls
EOF
kafkauser.kafka.strimzi.io/my-user created