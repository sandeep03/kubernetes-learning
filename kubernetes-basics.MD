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
  
