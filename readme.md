# Danny's Home Assignment
Steps
1. Run a docker file running Jenkins
2. Install basic plugins for Jenikins including Maven, Dependency checker and Artifactory
3. Create a pipeline job in Jenkins that clones the spring-petclinic project
4. Build a jenkinsfile script with four steps, Clone, Build, Scan and Upload to Artifactory
5. Create a Jfrog account on cloud env, create a repository for the Artifact and create and access token for Jenkins
6. integrate jenkins with Artifactory by configuring the plugin
7. Running the build
8. After cloning the project, the build is done on a docker image


## steps to create the docker:
Follow the manual from the official Jenkins site: https://www.jenkins.io/doc/book/installing/docker/

Runnable docker images are attached here
To load them:
docker import DockerExport1.tar jenkins-blueocean:v1
docker import DockerExport1.tar jenkins-docker:v1
docker run --it jenkins-blueocean:v1 sh
docker run --it jenkins-docker:v1 sh
the pipeline is called spring-petclinic


My Jfrog account is: https://dannyp.jfrog.io/
