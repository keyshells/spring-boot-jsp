pipeline {
    agent any

    tools {
        maven '3.8.5'
    }

    stages {
        stage('Source') {
            steps {
                git branch: 'develop', changelog: false, credentialsId: 'd0e97555-119c-44e5-87e9-9fb37ea9b239', poll: false, url: 'https://github.com/amalbinoy/spring-boot-jsp.git'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Deployment') {
            steps {
                sh '''
                    version=$(perl -nle 'print "$1" if /<version>(v\\d+\\.\\d+\\.\\d+)<\\/version>/' pom.xml)
                    java -jar -Dserver.port=8085 target/news-${version}.jar 
                '''
            }
        }
    }
}
