# Danny's Home Assignment
Steps
1. Run a docker file running Jenkins
2. Install basic plugins for Jenikins including Maven, Dependency checker and Artifactory
3. Create a pipeline job in Jenkins using the spring-petclinic project
4. Build a jenkinsfile script with four steps, Clone, Build, Scan and Upload to Artifactory
5. Create a Jfrog account on cloud env, create a repository for the Artifact and create and access token for Jenkins
6. integrate jenkins with Artifactory by configuring the plugin
7. Running the build
8. After cloning the project, the build is done on a docker image


## steps to create the docker from scratch:
Follow instructions on Jenkins website ([link](https://www.jenkins.io/doc/book/installing/docker/)) to run Jenkins on docker and a docker-in-docker container for the docker build step



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


