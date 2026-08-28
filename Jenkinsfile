pipeline {
    agent any

    tools {
        jdk 'java'       // Name from Jenkins Global Tool Config
        maven 'maven'    // Name from Jenkins Global Tool Config
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/bks-tech/simple-rest-war.git', branch: 'main'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // Example: copy WAR to Tomcat webapps
                sh '''
                cp target/*.war /opt/tomcat/webapps/
                '''
            }
        }
    }
}
