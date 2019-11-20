# outline-k8s
Some YAML templates to deploy [Outline](https://www.getoutline.com/) on [Kubernetes](https://kubernetes.io/)

## Prerequisite
- A Kubernetes cluster running
- [Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) or [Storage Class](https://kubernetes.io/docs/concepts/storage/storage-classes/) ready for use on the cluster (you'll need three PVs)

## Get these files
```shell=
git clone https://github.com/alfieyfc/outline-k8s.git
cd outline-k8s
```

## Set up your environment variables
1. Edit sensitive information in `outline-secrets.yaml` 
2. Edit `env` items in `outline-deploy.yaml` as you need, or you could simply use my ***slack*** setup (pun intended)

## Ready to go!
After completing the above section, just run:
```shell=
kubectl apply -f ./
```
Give it some time to deploy, it may take Outline a few restarts as it requires Postgres to be ready.

## Exposing your KB
You may expose your service in many ways. The easiest I have in mind is just running:
```shell=
kubectl -n outline-kb expose deploy outline-deploy --port 3000 --type NodePort
```
You may also want an [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/) resource in front of your [Service](https://kubernetes.io/docs/concepts/services-networking/service/), but I'll leave that to yourselves to figure out how. 
