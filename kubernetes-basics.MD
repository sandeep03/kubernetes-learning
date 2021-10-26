# Kubernetes basics modules
  1) Create a Kubernetes cluster
  2) Deploy an app
  3) Explore your app
  4) Expose your app
  5) Scale up your app
  6) Update your app
  
# Create a Kubernetes cluster
  A Kubernetes cluster consists of two types of resources:

  1) The Control Plane coordinates the cluster
  2) Nodes are the workers that run applications

  ![Alt text](/module_01_cluster.svg)
  
  The Control Plane is responsible for managing the cluster. 
  The Control Plane coordinates all activities in your cluster, such as scheduling applications, 
  maintaining applications' desired state, scaling applications, and rolling out new updates.

  A node is a VM or a physical computer that serves as a worker machine in a Kubernetes cluster. 
  Each node has a Kubelet, which is an agent for managing the node and communicating with the 
  Kubernetes control plane. The node should also have tools for handling container operations, 
  such as containerd or Docker. A Kubernetes cluster that handles production traffic should 
  have a minimum of three nodes.

  Control Planes manage the cluster and the nodes that are used to host the running applications.

  When you deploy applications on Kubernetes, you tell the control plane to start the 
  application containers. The control plane schedules the containers to run on 
  the cluster's nodes. The nodes communicate with the control plane using the Kubernetes API, 
  which the control plane exposes. End users can also use the 
  Kubernetes API directly to interact with the cluster.

  A Kubernetes cluster can be deployed on either physical or virtual machines. 
  To get started with Kubernetes development, you can use Minikube. 
  Minikube is a lightweight Kubernetes implementation that creates a VM on your local machine
  and deploys a simple cluster containing only one node. 
  Minikube is available for Linux, macOS, and Windows systems. 
  The Minikube CLI provides basic bootstrapping operations for 
  working with your cluster, including start, stop, status, and delete. 
  
  # Commands:
  Check minikube installation by running - minikube version

  Start the cluster, by running - minikube start
  
  Check kubectl installation by running - kubectl version

  To view the cluster details - kubectl cluster-info

  To view the nodes in the cluster - kubectl get nodes
  
  # Deploy an app
  Kubernetes Deployments
  
  Once you have a running Kubernetes cluster, you can deploy your containerized applications on top of it. To do so, you   create a Kubernetes Deployment configuration. The Deployment instructs Kubernetes how to create and update instances   of your application. Once you've created a Deployment, the Kubernetes control plane schedules the application           instances included in that Deployment to run on individual Nodes in the cluster.

Once the application instances are created, a Kubernetes Deployment Controller continuously monitors those instances. If the Node hosting an instance goes down or is deleted, the Deployment controller replaces the instance with an instance on another Node in the cluster. This provides a self-healing mechanism to address machine failure or maintenance.
  
  # Deploying your first app on Kubernetes
  
   ![Alt text](/module_02_first_app.svg)
   
   You can create and manage a Deployment by using the Kubernetes command line interface, **Kubectl** Kubectl uses the Kubernetes API to interact with the cluster. In this module, you'll learn the most common Kubectl commands needed to create Deployments that run your applications on a Kubernetes cluster.

When you create a Deployment, you'll need to specify the container image for your application and the number of replicas that you want to run.

For your first Deployment, you'll use a hello-node application packaged in a Docker container that uses NGINX to echo back all the requests. 
  
  # Commands:
  
  kubectl version
  
  kubectl get nodes --help
  
  deploy our first app on Kubernetes with the following:
  
  kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1

  kubectl get deployments

  Kubernetes cluster will be created but it will not be accessible to external world it can be done by creating proxy
  
  kubectl proxy

  check access to cluster
  curl http://localhost:8001/version

# Explore your app

Kubernetes Pods

![Alt text](/module_03_pods.svg)

A Pod is a Kubernetes abstraction that represents a group of one or more application containers (such as Docker), and some shared resources for those containers. Those resources include:

Shared storage, as Volumes
Networking, as a unique cluster IP address
Information about how to run each container, such as the container image version or specific ports to use

Pods are the atomic unit on the Kubernetes platform. When we create a Deployment on Kubernetes, that Deployment creates Pods with containers inside them (as opposed to creating containers directly). Each Pod is tied to the Node where it is scheduled, and remains there until termination (according to restart policy) or deletion. In case of a Node failure, identical Pods are scheduled on other available Nodes in the cluster.

Nodes

A Pod always runs on a Node. A Node is a worker machine in Kubernetes and may be either a virtual or a physical machine, depending on the cluster. Each Node is managed by the control plane. A Node can have multiple pods, and the Kubernetes control plane automatically handles scheduling the pods across the Nodes in the cluster. The control plane's automatic scheduling takes into account the available resources on each Node.

Every Kubernetes Node runs at least:

![Alt text](/module_03_nodes.svg)

Kubelet, a process responsible for communication between the Kubernetes control plane and the Node; it manages the Pods and the containers running on a machine.
A container runtime (like Docker) responsible for pulling the container image from a registry, unpacking the container, and running the application.

# Commands:

kubectl get - list resources

kubectl describe - show detailed information about a resource

To get the Pod name and store it in the POD_NAME environment variable:

export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')

echo Name of the Pod: $POD_NAME

To see the output of our application, run a curl request.

curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/

kubectl logs - print the logs from a container in a pod

Next let’s start a bash session in the Pod’s container:

kubectl exec -ti $POD_NAME -- bash
