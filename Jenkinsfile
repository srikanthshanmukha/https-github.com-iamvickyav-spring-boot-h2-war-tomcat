parameters {
  choice choices: ['dev', 'qa', 'prod'], description: 'select environment', name: 'Env'
}
pipeline {
    agent any
    tools {
        maven 'MAVEN_PATH'
        jdk 'jdk8'
    }
    stages {
        stage("Tools initialization") {
            steps {
                sh "mvn --version"
                sh "java -version"
            }
        }
        stage("Checkout Code") {
            steps {
                checkout scm
            }
        }
        stage('Build and deploy to development') {
            when {
                expression { 
                   return params.ENVIRONMENT == 'dev'
                }
            }
            steps {
                    sh "mvn package"
                    sh "mvn tomcat7:deploy"
                }
            }
         stage('Build and deploy to QA') {
            when {
                expression { 
                   return params.ENVIRONMENT == 'qa'
                }
            }
            steps {
                    sh "mvn package"
                    sh "mvn tomcat7:deploy"
                }
            }
          stage('Build and deploy to Production') {
            when {
                expression { 
                   return params.ENVIRONMENT == 'prod'
                }
            }
            steps {
                    sh "mvn package"
                    sh "mvn tomcat7:deploy"
                }
            }
        }
    }
