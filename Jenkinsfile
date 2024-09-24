pipeline {
    agent any
    tools {
        maven 'MAVEN'
    }
    stages {
        stage("Clone Code") {
            steps {
                git branch: 'main', credentialsId: 'nkosi_github', url: 'https://github.com/Nkossyk95/Springboot-demo.git'
            }
        }
        stage("Build Code") {
            steps {
                sh 'mvn clean install'
            }
        }
        stage("Copy JAR and Restart Application") {
            steps {
                script {
                    def jarFile = 'app/target/springboot-demo.jar'
                    def destinationDir = '/data/jars'

                    sh "sudo cp ${jarFile} ${destinationDir}/"

                    sh 'sudo systemctl restart springboot-demo-nkosi.service'
                }
            }
        }
    }
}