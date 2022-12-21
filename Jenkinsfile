pipeline {
    agent any

 environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
    stages {
        stage('Pull-Tag-Push') {
            steps {
                sh "jf docker pull jf docker pull danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:latest"
                sh "jf docker tag $JPD/$DEVREPO/$SRCCTR:$DOCKERTAG $JPD/$DEVREPO/$PRJ:$JFROG_CLI_BUILD_NUMBER"
                sh "jf docker push danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:latest --build-name=petclinic --build-number=1"
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
