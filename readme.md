# Danny's Home Assignment
Steps:
1. Follow instructions on Jenkins website ([link](https://www.jenkins.io/doc/book/installing/docker/)) to run Jenkins on Docker and a Docker-in-Docker container for the Docker build step
1. Install basic plugins for Jenkins including Maven, Dependency checker and Artifactory
1. Create a Jfrog account on cloud env, create a repository for the Artifact and create and access token for Jenkins
1. Integrate Jenkins with Artifactory by configuring the plugin
1. Create DockerHub account with petclinic repository
1. Add DockerHub user and password credentials to Jenkins "Credentials Manager"
1. Create a pipeline job in Jenkins for spring-petclinic project and use the Jenkinsfile in this repo (CSM type: Git)
1. Run a build
1. The build will clone, build, docker build and docker push an image to dockerhub ([link](https://hub.docker.com/repository/docker/dannyparizada/dockerhubrepo))


My Jfrog account is: https://dannyp.jfrog.io/


To allow Jenkins to access docker
```
docker run \                    
  --name jenkins-docker \
  --rm \
  --detach \
  --privileged \
  --network jenkins \
  --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --publish 2376:2376 \
  docker:dind \
  --storage-driver overlay2
```

To run Jenkins in docker (this is already pre-build in my docker hub - dockerfile below):
```
docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  dannyparizada/jenkins-blueocean:2.361.2-1 
```

Dockerfile for Jenkins:
```
FROM jenkins/jenkins:lts-jdk11
USER root
RUN apt-get update && apt-get install -y lsb-release
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce-cli
USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean:1.25.8 docker-workflow:521.v1a_a_dd2073b_2e"
```

To run the petclinic image `docker run -p 8081:8080 dannyparizada/spring-petclinic`
and direct your browser to http://localhost:8081
