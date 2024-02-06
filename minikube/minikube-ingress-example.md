## Enable ingress addon

$ minikube addons enable ingress

##### Apply deployment for Ingress from minikube directory
kubectl apply -f minikube-ingress-deployment-example.yaml

**OR the same command with deployment.yaml online**
$ kubectl apply -f https://storage.googleapis.com/minikube-site-examples/ingress-example.yaml

**Get Ingress address**
$ kubectl get ingress


**Note for Docker Desktop Users:**

To get ingress to work you’ll need to open a new terminal window and run:   
`$ minikube tunnel`

and in the following step use 127.0.0.1 in place of <ip_from_above>.  
`$  curl 127.0.0.1/bar   
$  curl 127.0.0.1/foo`


**For NOT DOCKER DESKTOP Now verify that the ingress works**

$ curl <ip_from_above>/foo  
Request served by foo-app
...

$ curl <ip_from_above>/bar  
Request served by bar-app