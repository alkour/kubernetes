## kubernetes

This the tutorial from spring.io
https://spring.io/guides/gs/spring-boot-kubernetes

#### Step 1. Download SpringBoot App with WebFlux, Actuator

Dowload from start.spring.io

Or using curl commandcurl https://start.spring.io/starter.tgz -d dependencies=webflux,actuator | tar -xzvf -

1. Build the application, I use Idea Gradle` bootJar` task in Idea Gradle Tool, or `./gradlew bootJar`   
2. Run `java -jar build/libs/springBooToKuber-0.0.1-SNAPSHOT.jar`
3. Check app  `curl localhost:8080/actuator` in GitBash OR `curl` Enter,  then URL:` http://localhost:8080/actuator`   
Enter

#### Containerize the Application

`./gradlew bootBuildImage`  build docker image  by using Gradle plugin

1. Run  `docker image ls` to see image  created
2. Run docker run -p  8080:8080 springboot-to-kuber:0.0.1-SNAPSHOT to start image in container
3. Check app  `curl localhost:8080/actuator` in GitBash, then delete container
4. Add tag  `docker tag springboot-to-kuber:0.0.1-SNAPSHOT springguides/kuber_demo`
5. Push images to docker  registry (DockerHub) springguides/kuber_demo  For testing on local machine, this step in not required.

#### Deploy the Application to Kubernetes  
Run dry-run command to create deployment.yaml in root folder   
`kubectl create deployment demo --image=springguides/kuber_demo --dry-run=client -o=yaml > deployment.yaml`

Run to add `echo --- >> deployment.yaml`  --- deployment.yaml file

Run command to add service to deployment
`kubectl create service clusterip demo --tcp=8080:8080 --dry-run=client -o=yaml >> deployment.yaml`

Deploy service to minikube from deployment.yaml
`kubectl apply -f deployment.yaml`

eval $(minikube docker-env)
Usage
Start a cluster using the docker driver:

minikube start --driver=docker //Did it
To make docker the default driver:

minikube config set driver docker //Check it and do if it  works correctly
   








