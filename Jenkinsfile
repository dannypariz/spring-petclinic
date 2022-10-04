pipeline {
    agent any
    tools {
        maven "M3"
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
    }
}
