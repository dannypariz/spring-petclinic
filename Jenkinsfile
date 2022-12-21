pipeline {
    agent any

 environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
    stages {
        stage('Clone) {
            steps {
                sh "jf docker pull danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:latest"
                sh "echo 'Clone completed'"
            }
        }
        
     stage('Build') {
            steps {
                sh "echo building the image"
                sh "echo building complete"
            }
        }
                   
     stage('Deploy') {
            steps {
                  sh "jf docker tag danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:latest danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:2.2"
                  sh "jf docker push danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:2.2 --build-name=petclinic --build-number=2"
        
        
    stages {
        stage('Publish') {
            steps {
                sh "jf rt build-publish danpar.jforg.io/dojo-dev-docker/dannyparizada/spring-petclinic:1"
            }
        }
        
        
        stage('Publish') {
            steps {
                sh "jf rt build-publish petclinic 3 "
            }
        }
        stage('Scan') {
            steps {
                sh "jf docker scan danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:2.2"
                sh "jf build-scan petclinic 2"
    }
  }
}
