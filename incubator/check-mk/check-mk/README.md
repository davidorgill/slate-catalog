# Check-mk
This project provides monitoring services for a kubernetes cluster with [SLATE](http://slateci.io/).

## Minimum Requirements - - - - - I may need to update this based on slate application
- Linux (2 cores, 4GB memory, 15GB storage) or MacOS
- A publicly accessible IP address (port 6443 open)
- Python (3 or 2.7, 'python' must be in your PATH)
- [DockerCE](https://docs.docker.com/install/#supported-platforms)
- [Docker-Compose](https://github.com/docker/compose/releases) (installed with Docker for Mac)
-Possibly need to install helm and tiller(Refer back to this note) and SLATE application

On Linux, the user running SLATElite must be a member of the Docker group (or root).
Users can be added to the Docker group with: `sudo usermod -a -G docker <username>`

## Getting Started
After installing the dependency requirements and pulling the SLATElite repository:


//////////////////////////////////////////////////////////////////
////////Everything that is requires to get slate up and going///
//////////////////////////////////////////////////////////////////.


##Deploying Check-mk in your kubernetes cluster once you've established your cluster

Clone the [slateci/slate-catalog](https://github.com/slateci/slate-catalog) repository on the machine you are running your Kubernestes cluster on.

cd into your slate-catalog/incubator/check-mk/check-mk directory. At this point you will need to deploy the check-mk application within Kubernetes. To do this run `helm install check-mk`. Helm manages the deployement of check-mk.

Run `kubectl get pods` to ensure that the check-mk application is now running on your cluster. You should see a pod that has been deployed and is running check-mk.

In order to set up the dashboard that you will be running to monitor your cluster you need to run the following commands
`export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services check-mk-global)`
`export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")`
`echo http://$NODE_IP:$NODE_PORT/cmk/check_mk`




