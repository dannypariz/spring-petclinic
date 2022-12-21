pipeline {
    agent any

 environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
    stages {
        stage('Clone) {
            steps {
                sh "jf docker pull jf docker pull danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:latest"
                sh "echo Clone completed"
            }
        }
        
     stage('Build') {
            steps {
                sh "echo building the image"
                sh "jf rt build-publish $JFROG_CLI_BUILD_NAME $JFROG_CLI_BUILD_NUMBER"
                sh "echo building complete"
            }
        }
                   
     stage('Deploy') {
            steps {
                  sh "jf docker tag danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:1 
                  sh "jf docker push danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:1 --build-name=petclinic --build-number=1"
        
        
    stages {
        stage('Publish') {
            steps {
                sh "jf rt build-publish danpar.jforg.io/dojo-dev-docker/dannyparizada/spring-petclinic:1"
            }
        }
        
        
        stage('Publish') {
            steps {
                sh "jf rt build-publish $JFROG_CLI_BUILD_NAME $JFROG_CLI_BUILD_NUMBER"
            }
        }
        stage('Scan') {
            steps {
                sh "jf docker scan $JPD/$DEVREPO/$PRJ:$JFROG_CLI_BUILD_NUMBER --format=json"
    }
  }
}
