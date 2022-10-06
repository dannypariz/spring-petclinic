# Danny's Home Assignment
Steps:
1. Follow instructions on Jenkins website ([link](https://www.jenkins.io/doc/book/installing/docker/)) to run Jenkins on Docker and a Docker-in-Docker container for the Docker build step
1. Install basic plugins for Jenkins including Maven, Dependency checker and Artifactory
1. Create a Jfrog account on cloud env, create a repository for the Artifact and create and access token for Jenkins
1. Integrate Jenkins with Artifactory by configuring the plugin
1. Create a pipeline job in Jenkins for spring-petclinic project and use the Jenkinsfile in this repo
1. Run a build
1. The build will clone, build, docker build and docker push an image to dockerhub ([link](https://hub.docker.com/repository/docker/dannyparizada/dockerhubrepo))



## steps to create the docker from runnable image:

* Runnable docker images are attached here
* Number of files: 2 (1.00GB)
* Link: https://jumbomail.me/j/7HjrwoqLnUCgaVS
* Expiration date: 2022-10-12


To load them:

```
docker import DockerExport1.tar jenkins-blueocean:v1
docker import DockerExport1.tar jenkins-docker:v1
docker run --it jenkins-blueocean:v1 sh
docker run --it jenkins-docker:v1 sh
```
The pipeline is called spring-petclinic


My Jfrog account is: https://dannyp.jfrog.io/


