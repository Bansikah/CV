---
title: "Kubernetes for Beginners"
datePublished: Wed May 22 2024 22:33:19 GMT+0000 (Coordinated Universal Time)
cuid: clwiehflx00020amff5ejarn1
slug: kubernetes-for-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1716417057449/0210ee4a-1495-4e23-ba83-10664ed1ed2c.png
tags: kubernetes, devops, orchestration, cic

---

## Table of Contents for Article on Kubernetes

* Introduction to Kubernetes
    
* Overview of container orchestration
    
* Benefits of using Kubernetes
    

* Kubernetes Architecture
    
* Master and Worker Nodes
    
* Control Plane Components
    
* Data Plane Components
    

* Deploying Applications on Kubernetes
    
* Pods
    
* Deployments
    
* Services
    
* Ingress
    

* Scaling and Load Balancing
    
* Horizontal Pod Autoscaling (HPA)
    
* Cluster Autoscaler
    
* Load Balancing with Services
    

* Storage and Persistence
    
* Persistent Volumes (PVs)
    
* Persistent Volume Claims (PVCs)
    
* StatefulSets
    

* Networking
    
* Networking models in Kubernetes
    
* Service Discovery and DNS
    
* Network policies
    

* Security and Access Control
    
* RBAC (Role-Based Access Control)
    
* Secrets
    
* Network policies
    

* Monitoring and Logging
    
* Kubernetes Metrics
    
* Prometheus and Grafana
    
* Logging with Elasticsearch and Kibana
    

* Troubleshooting and Debugging
    
* Common issues and solutions
    
* kubectl commands for debugging
    
* Kubernetes events
    

* Advanced Topics
    
* StatefulSets and Stateful Applications
    
* DaemonSets
    
* Taints and Tolerations
    
* Custom Resource Definitions (CRDs)
    
* Operators
    

# 1\. Introduction to Kubernetes

Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications. It was originally developed by Google and is now maintained by the Cloud Native Computing Foundation (CNCF).

# Key features of Kubernetes include

* **Containerization**: Kubernetes allows you to package your applications into containers, ensuring consistency and portability across different environments.
    
* **Automated deployment and scaling**: Kubernetes automatically deploys and scales containerized applications based on resource utilization and defined policies.
    
* **Service discovery and load balancing**: Kubernetes provides built-in service discovery and load balancing, enabling applications to communicate with each other efficiently.
    
* **Self-healing**: Kubernetes automatically recovers from failures, such as node failures or container crashes, by rescheduling and restarting containers.
    
* **Rolling updates and rollbacks**: Kubernetes supports rolling updates and rollbacks, allowing you to deploy new versions of your applications without downtime.
    

**Example Code:**

```plaintext
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app:1.0
        ports:
        - containerPort: 8080
```

**2\. Kubernetes Architecture**

Kubernetes consists of a master node and multiple worker nodes. The master node manages the cluster, while the worker nodes run the containerized applications.

![Image description](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zkvlzhatt44mwcywncu7.png align="left")

**Control Plane Components:**

`kube-apiserver:` Exposes the Kubernetes API, allowing clients to interact with the cluster. `kube-scheduler:` Assigns pods to worker nodes based on resource availability and defined policies. `kube-controller-manager:` Manages various controllers, such as replication controllers and endpoints controllers. `etcd:` A distributed key-value store that stores the cluster's state and configuration.

**Data Plane Components:**

`kubelet:` An agent running on each worker node that manages containers and communicates with the control plane. `kube-proxy:` A network proxy that load balances traffic between pods and provides network connectivity for services. `Container runtime:` The software responsible for running containers, such as Docker or containerd.

**Example Code:**

```plaintext
# List all Kubernetes components
kubectl get componentstatuses

# View the status of nodes in the cluster
kubectl get nodes
```

**3\. Deploying Applications on Kubernetes**

To deploy applications on Kubernetes, you need to create Kubernetes manifests, such as Deployment, Service, and Ingress resources.

**Pods:**

Pods are the smallest unit of deployment in Kubernetes, representing a single instance of an application. They can contain one or more containers that are tightly coupled and share resources.

**Example Code:**

```plaintext
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: my-container:1.0
    ports:
    - containerPort: 8080
```

**Deployments:**

Deployments manage the lifecycle of Pods and provide features like scaling, rolling updates, and rollbacks.

**Example Code:**

```plaintext
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app:1.0
        ports:
        - containerPort: 8080
```

**Services:**

Services provide network access to Pods within the cluster. They can be exposed using different types, such as ClusterIP, NodePort, or LoadBalancer.

**Example Code:**

```plaintext
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

**Ingress:**

Ingress allows external traffic to reach services running in the cluster. It provides a way to configure routing rules and load balancing.

**Example Code:**

```plaintext
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: my-app.example.com
    http:
      paths:
      - path: /
        backend:
          serviceName: my-service
          servicePort: 80
```

**4\. Scaling and Load Balancing**

Kubernetes provides features to scale applications and distribute traffic efficiently.

**Horizontal Pod Autoscaling (HPA):**

HPA automatically scales the number of Pods based on CPU or custom metrics.

**Example Code:**

```plaintext
apiVersion: autoscaling/v2beta2
kind: HorizontalPodAutoscaler
metadata:
  name: my-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  minReplicas: 3
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
```

**Cluster Autoscaler:**

Cluster Autoscaler automatically scales the number of worker nodes in the cluster based on resource utilization.

**Example Code:**

To use Cluster Autoscaler, you need to install and configure it separately.

**Load Balancing with Services:**

Services in Kubernetes provide load balancing by distributing traffic across multiple Pods. By default, Kubernetes uses a round-robin algorithm for load balancing.

**Example Code:**

See the example code for creating a Service in the previous section.

**5\. Storage and Persistence**

Kubernetes provides various storage options to persist data for applications.

**Persistent Volumes (PVs):**

PVs are abstract storage resources that can be provisioned by different storage providers, such as local storage, network storage, or cloud storage.

**Example Code:**

```plaintext
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```

**Persistent Volume Claims (PVCs):**

PVCs are requests for storage resources, allowing applications to consume PVs without knowing their specific details.

**Example Code:**

```plaintext
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
```

**StatefulSets:**

StatefulSets are used for managing stateful applications, such as databases or message queues. They ensure that Pods maintain a unique identity and persistent storage.

**Example Code:**

```plaintext
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: my-stateful-set
spec:
  serviceName: "my-service"
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: my-app:1.0
        ports:
        - containerPort: 8080
        volumeMounts:
        - name: my-volume
          mountPath: /data
  volumeClaimTemplates:
  - metadata:
      name: my-volume
    spec:
      accessModes: [ "ReadWriteOnce" ]
      resources:
        requests:
          storage: 1Gi
```

**6\. Networking**

Kubernetes provides various networking options to enable communication between Pods and external services.

**Networking models in Kubernetes:**

`Container-to-Container Networking:` Kubernetes provides a flat network for Pods, allowing them to communicate directly with each other using IP addresses. `Pod-to-Service Networking:` Kubernetes provides a virtual IP address for each Service, enabling Pods to communicate with each other using the Service's IP address. `External-to-Service Networking:` Kubernetes provides a way to expose Services to external traffic using different networking options, such as NodePort, LoadBalancer, or Ingress.

**Example Code:**

See the example code for creating a Service in the previous section.

**Service Discovery and DNS:**

Kubernetes provides built-in service discovery using DNS. Services can be accessed using their DNS names, which are automatically created by Kubernetes.

**Example Code:**

```plaintext
# Access a Service using its DNS name
kubectl run -it --rm --restart=Never --image=alpine dns-test -- nslookup my-service
```

**Network policies:**

Network policies allow you to control the traffic flow between Pods and Services based on defined rules.

**Example Code:**

```plaintext
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: my-network-policy
spec:
  podSelector:
    matchLabels:
      app: my-app
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: my-app
    ports:
    - protocol: TCP
      port: 80
```

**7\. Security and Access Control**

Kubernetes provides various security features to protect your cluster and applications.

**Role-Based Access Control (RBAC):**

RBAC allows you to define fine-grained access control policies for Kubernetes resources.

**Example Code:**

```plaintext
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: my-role
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: my-role-binding
subjects:
- kind: User
  name: my-user
  apiGroup: ""
roleRef:
  kind: Role
  name: my-role
  apiGroup: ""
```

**Secrets:**

Secrets allow you to store sensitive information, such as passwords, API keys, or certificates, in Kubernetes.

**Example Code:**

```plaintext
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  username: bXktYXBw
  password: cGFzc3dvcmQx
```

**Network policies:**

See the example code for creating a NetworkPolicy in the previous section.

**8\. Monitoring and Logging**

Kubernetes provides various monitoring and logging solutions to help you observe and troubleshoot your cluster and applications.

**Kubernetes Metrics:**

Kubernetes provides built-in metrics, such as CPU and memory usage, for Pods and Nodes. You can use tools like Prometheus and Grafana to collect and visualize these metrics.

**Example Code:** **View CPU and memory usage for all Pods**

```plaintext
kubectl top pods
```

**View CPU and memory usage for a specific Pod**

```plaintext
kubectl top pod my-pod
```

**Prometheus and Grafana:**

Prometheus is an open-source monitoring and alerting system, while Grafana is a visualization tool for time series data. You can use these tools to collect and visualize metrics from your Kubernetes cluster.

Example Code:

To install Prometheus and Grafana, you can use Helm, a package manager for Kubernetes. **Add the Prometheus Helm repository**

```plaintext
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```

**Install Prometheus**

```plaintext
helm install prometheus prometheus-community/prometheus
```

**Add the Grafana Helm repository**

```plaintext
helm repo add grafana https://grafana.github.io/helm-charts
```

**Install Grafana**

```plaintext
helm install grafana grafana/grafana
```

**Logging with Elasticsearch and Kibana**:

Elasticsearch is a distributed search and analytics engine, while Kibana is a visualization tool for Elasticsearch. You can use these tools to collect and analyze logs from your Kubernetes cluster.

**Example Code:**

To install Elasticsearch and Kibana, you can use Helm, a package manager for Kubernetes. **Add the Elastic Helm repository**

`helm repo add elastic` [`https://helm.elastic.co/helm`](https://helm.elastic.co/helm)

**Install Elasticsearch**

`helm install elasticsearch elastic/elasticsearch`

**Install Kibana** `helm install kibana elastic/kibana`

**9\. Troubleshooting and Debugging**

Kubernetes provides various tools and techniques to troubleshoot and debug your applications.

**Common issues and solutions:**

**Pods are not running:** Check the Pod's status using kubectl describe pod my-pod and look for any errors or warnings. Services are not accessible: Check the Service's status using kubectl describe service my-service and ensure that the correct ports and targetPort are configured. Resource limits and requests: Ensure that your Pods have appropriate resource limits and requests defined to prevent resource contention.

**kubectl commands for debugging:**

```plaintext
kubectl get pods: List all Pods in the current namespace.
kubectl describe pod my-pod: View detailed information about a specific Pod.
kubectl logs my-pod: View the logs of a specific Pod.
kubectl exec -it my-pod -- sh: Execute a shell inside a specific Pod.
kubectl apply -f my-manifest.yaml: Apply a Kubernetes manifest file.
kubectl delete -f my-manifest.yaml: Delete a Kubernetes manifest file.
```

**Kubernetes events:**

Kubernetes events provide insights into the lifecycle of objects in the cluster. You can use the kubectl get events command to view events and identify potential issues.

Example Code: **View Kubernetes events**

```plaintext
kubectl get events
```

**10\. Advanced Topics**

**StatefulSets and Stateful Applications:** Learn how to manage stateful applications, such as databases or message queues, in Kubernetes. **DaemonSets**: Learn how to run a single instance of a Pod on each node in the cluster, such as a monitoring agent or log collector. **Taints and Tolerations:** Learn how to schedule Pods to specific nodes based on their taints and tolerations. Custom Resource Definitions (CRDs): Learn how to extend Kubernetes by defining custom resources and controllers. **Operators:** Learn how to build and manage applications using Operators, which automate the management of complex stateful applications.

**Conclusion**

Kubernetes is a powerful and versatile container orchestration platform that provides a foundation for building and managing scalable and resilient applications. In this article, we have explored various aspects of Kubernetes, including its architecture, deployment, scaling, storage, networking, security, monitoring, troubleshooting, and advanced topics.

By understanding the concepts and best practices outlined in this guide, you can effectively leverage Kubernetes to build and manage containerized applications. As you continue to explore Kubernetes, remember to stay updated with the latest features, best practices, and community resources.

If you have any specific questions or need further assistance, feel free to reach out to the Kubernetes community or consult the official documentation and also post your comments in the comments section for any challenges.

Also, feel free to custumize and change the port numbers to suit your preferred port, you can use simple images like nginx and so on.

Happy containerizing and orchestrating!

**References**

Kubernetes Documentation: [https://kubernetes.io/docs/home/](https://kubernetes.io/docs/home/) Kubernetes Tutorials: [https://kubernetes.io/docs/tutorials/](https://kubernetes.io/docs/tutorials/) Kubernetes Community: [https://kubernetes.io/community/](https://kubernetes.io/community/) Prometheus: [https://prometheus.io/](https://prometheus.io/) Grafana: [https://grafana.com/](https://grafana.com/) Elasticsearch: [https://www.elastic.co/elasticsearch/](https://www.elastic.co/elasticsearch/) Kibana: [https://www.elastic.co/kibana](https://www.elastic.co/kibana) Helm: [https://helm.sh/](https://helm.sh/) Prometheus Helm Chart: [https://github.com/prometheus-community/helm-charts/tree/main/prometheus](https://github.com/prometheus-community/helm-charts/tree/main/prometheus) Grafana Helm Chart: [https://github.com/grafana/helm-charts/tree/main/grafana](https://github.com/grafana/helm-charts/tree/main/grafana) Elasticsearch Helm Chart: [https://github.com/elastic/helm-charts/tree/main/elasticsearch](https://github.com/elastic/helm-charts/tree/main/elasticsearch) Kibana Helm Chart: [https://github.com/elastic/helm-charts/tree/main/kibana](https://github.com/elastic/helm-charts/tree/main/kibana) RBAC: [https://kubernetes.io/docs/reference/access-authn-authz/rbac/](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) Network Policies: [https://kubernetes.io/docs/concepts/services-networking/network-policies/](https://kubernetes.io/docs/concepts/services-networking/network-policies/) StatefulSets: [https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) DaemonSets: [https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) Taints and Tolerations: [https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) Custom Resource Definitions (CRDs): [https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) Operators: [https://kubernetes.io/docs/concepts/extend-kubernetes/operator/](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/)