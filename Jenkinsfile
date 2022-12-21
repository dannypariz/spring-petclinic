pipeline {
    agent any
 environment {
    CI = true
    //ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
  
 
    stages {
        stage('Clone') {
            steps {
                sh "jf config use danpar"
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
                  sh "jf docker tag danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:latest danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:${BUILD_NUMBER}"
                  sh "jf docker push danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:${BUILD_NUMBER} --build-name=petclinic --build-number=${BUILD_NUMBER}"
            }
        }
        
        stage('Publish') {
            steps {
                sh "jf rt build-publish petclinic ${BUILD_NUMBER} "
            }
        }
        stage('Scan') {
            steps {
                sh "jf docker scan danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:${BUILD_NUMBER}"
                //sh "jf build-scan petclinic 4"
            }
        }
    }
 }
