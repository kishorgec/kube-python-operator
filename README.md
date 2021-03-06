## Kubernetes Python Operator

A Kubernetes operator is a high-level description of a deployable application to be run in a Kubernetes cluster. This is a tiny Kubernetes operator written in **Python** to set default cpu and memory limits on every deployment and statefulset that doesn't have them.

### How it Works
---

- Operator fetch the current deployments or statefulset objects from the namespace provided and updates them with CPU and Memory resources we specified the in config [file](conf/config.py) for those which haven't them by default.

### Usage
---

- The operator can be approached in many ways.
1) Can be used as a static operator to be run in the local machine where you make the kubectl commands.
```
python deployment_operator.py
```

2) A [watchable operator](watch_deployment_operator.py) is added which will monitor the deployments inside the namespace provided in realtime and updates the deployment whenever a new object is registered to the cluster.

3) Create the docker image of the operator (sample [dockerfile](Dockerfile) provided) and a Kubernetes [cronjob](cronjob.yaml) scheduled to run in a namespace at a specific time such that our operator itself will be running inside a pod in cluster.



### How to Run
---

- Clone the repo to your system by `git clone https://github.com/kishorgec/kudo-python-operator.git`

- Make sure that you have the latest **kubectl** installed on the client machine. Kubectl is a command line tool for controlling Kubernetes clusters. kubectl looks for a file named config in the $HOME/.kube directory.

- Type commands
```
python deployment_operator.py    // for managing deployment objects in the namespace

python statefulset_operator.py   // for managing statefulset objects in the namespace

python watch_deployment_operator.py
```
