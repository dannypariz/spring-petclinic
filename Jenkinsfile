pipeline {
    agent any
    tools {
        maven "M3"
    }
 environment {
    CI = true
    CLI_ID = 'danpar' 
    JPD = 'danpar.jfrog.io'
    DEVREPO = 'dojo-dev-docker'
    TESTREPO = 'dojo-test-docker'
    QAREPO = 'dojo-qa-docker'
    PRODREPO = 'dojo-prod-docker'
    PRJ = 'dannyparizada/petclinic'
    JFROG_CLI_ENV_EXCLUDE = ';VSCODE*;*ASKPASS;*EXCLUDE'
    //ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
  }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/dannypariz/spring-petclinic.git'
                sh "mvn clean install -Dcheckstyle.skip"
            }
        }
         stage('Build') {
            steps {
                sh "docker build --build-arg JAR_FILE=target/*.jar -t dannyparizada/spring-petclinic ."
            }
        }
                   
         stage('Deploy') {
            steps {
                  sh "jf c use danpar"
                  sh "jf docker tag danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:latest danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:${BUILD_NUMBER}"
                  sh "jf docker push danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:${BUILD_NUMBER} --build-name=${JOB_NAME} --build-number=${BUILD_NUMBER}"
            }
        }
        
        stage('Collect') {
            steps {
                sh "jf rt build-collect-env ${JOB_NAME} ${BUILD_NUMBER}"
            }
        }
        
        stage('Publish') {
            steps {
                sh "jf rt build-publish ${JOB_NAME} ${BUILD_NUMBER}"
            }
        }
        stage('Promote to Test') {
            steps {
                sh "jf rt build-promote ${JOB_NAME} ${BUILD_NUMBER} ${TESTREPO} --status TEST --comment 'unit tests successul'"
            }
        }
        stage('Docker Scan') {
            steps {
                sh "jf docker scan danpar.jfrog.io/dojo-dev-docker/dannyparizada/spring-petclinic:${BUILD_NUMBER} --vuln"
            }
        }
        stage('Promote to QA') {
            steps {
                sh "jf rt build-promote ${JOB_NAME} ${BUILD_NUMBER} ${QAREPO} --status QA --comment 'security checks successful'"
            }
        }
        stage('Build Scan') {
            steps {
                sh "jf build-scan ${JOB_NAME} 21 --fail=false"
            }
        }
        stage('Promote to Prod') {
            steps {
                sh "jf rt build-promote ${JOB_NAME} ${BUILD_NUMBER} ${PRODREPO} --status PROD --comment 'currently in production'"
            }
        }
    }
 }
