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
4. Add tag in order  to push to  private repo  `docker tag springboot-to-kuber:0.0.1-SNAPSHOT climbingdock/springboot-to-kuber`
5. Push images to docker  registry (DockerHub) `docker push climbingdock/springboot-to-kuber`

#### Deploy the Application to Kubernetes

To make deployment.yaml
1. Run dry-run command to create deployment.yaml in root folder `kubectl create deployment demo --image=climbingdock/springboot-to-kuber --dry-run=client -o=yaml > deployment.yaml`
2. Run to add `echo --- >> deployment.yaml`  --- deployment.yaml file
3. Run command to add service to deployment `kubectl create service clusterip demo --tcp=8080:8080 --dry-run=client -o=yaml >> deployment.yaml`

**As result deployment.yaml is created  on local computer**
Deploy service to minikube from deployment.yaml
`kubectl apply -f deployment.yaml`

Port-forward to create ssh tunnel
`kubectl port-forward svc/demo 8080:8080` 

Test `$ curl localhost:8080/actuator/health`

####  Point-to-Remember:  
It seems that minikube can not image from DockerDesktop of local computer
