# Kubernetes Architecture

## Two Parts: Control Plane + Worker Nodes

## Control Plane Components
| Component | What it does |
|---|---|
| API Server | Single entry point for all cluster communication |
| etcd | Distributed key-value store — stores ALL cluster desired state |
| Scheduler | Decides which node a pod runs on |
| Controller Manager | Runs all controllers — reconciles actual vs desired state |
| Cloud Controller Manager | Talks to cloud provider APIs (Azure, AWS, GCP) |

## Worker Node Components
| Component | What it does |
|---|---|
| kubelet | Agent on every node — ensures pods run as declared |
| kube-proxy | Manages network rules for Services on each node |
| Container Runtime (containerd) | Actually runs the containers |

## AKS — Who Manages What
| Component | Manager |
|---|---|
| API Server, etcd, Scheduler, Controller Manager | Microsoft |
| Worker nodes, kubelet, kube-proxy, workloads | You |

## What Happens When You Run kubectl apply
1. kubectl → API Server (authenticated request)
2. API Server → validates and stores in etcd
3. Controller Manager detects new desired state
4. Scheduler assigns pod to a node
5. kubelet on that node receives the pod spec
6. kubelet tells containerd to start the container

## Interview Answer
Kubernetes has two parts — control plane and worker nodes. Control plane: API Server (single entry point), etcd (desired state store), Scheduler (pod placement), Controller Manager (reconciliation loops). Worker nodes: kubelet (ensures pods run), kube-proxy (Service networking), container runtime (runs containers). In AKS, Microsoft manages the control plane — we manage node pools and workloads.

## Quick Revision (Flashcards)
Q: What is the single entry point for all Kubernetes communication?
A: API Server

Q: Where is cluster desired state stored?
A: etcd

Q: Which component places pods on nodes?
A: Scheduler

Q: Which component on a worker node ensures containers are running?
A: kubelet

Q: Which component created the Azure Load Balancer when you created a K8s Service?
A: Cloud Controller Manager

Q: etcd goes down. What breaks?
A: No new changes can be made. Existing pods keep running. Cluster brain is gone.
