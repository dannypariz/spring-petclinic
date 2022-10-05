pipeline {
    agent any
    tools {
        maven "M3"
    }
 environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }
    stages {
        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/dannypariz/spring-petclinic.git'
                sh "mvn clean install -Dcheckstyle.skip"
                //sh "java -jar target/*.jar"

            }
        }
        stage('Build') {
            steps {
                //sh "./mvnw spring-boot:build-image -Dcheckstyle.skip"
                sh "docker build --build-arg JAR_FILE=target/*.jar -t danny/petclinic ."
            }
        }
        stage('Scan') {
            steps {
                dependencyCheck additionalArguments: '''
                    -o "./"
                    -s "./"
                    -f "ALL"
                    --prettyPrint''', odcInstallation: 'Dependency-Check'

                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
        stage('Upload to Artifactory') {
      agent {
        docker {
          image 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0' 
          reuseNode true
        }
      }
      steps {
        sh 'jfrog rt upload --url https://dannyp.jfrog.io/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} target/demo-0.0.1-SNAPSHOT.jar java-web-app/'
      }
    }
  }
}
