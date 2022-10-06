pipeline {
    agent any
    tools {
        maven "M3"
    }
 environment {
    CI = true
    ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
    dockerhub = credentials('dockerhub')
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
        stage('Build') {
            steps {
                //sh "./mvnw spring-boot:build-image -Dcheckstyle.skip"
                sh "docker build --build-arg JAR_FILE=target/*.jar -t dannyparizada/spring-petclinic ."
                sh "echo $dockerhub_PSW | docker login -u $dockerhub_USR --password-stdin"
                sh "docker push dannyparizada/spring-petclinic"
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
                  sh 'jfrog rt upload --url https://dannyp.jfrog.io/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} Jenkinsfile spring-petclinic/'
      }
    }
  }
}
