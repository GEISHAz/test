pipeline {
    agent any
    tools {
        gradle 'gradle'
    }
    stages {
        stage('clone'){
            steps{
                git branch: 'main', url: 'https://github.com/GEISHAz/test.git'
            }
        }
        stage('Gradle build') {
                steps {
                    dir('./testserver') {
                            sh 'chmod +x ./gradlew'
        					sh './gradlew clean build'
                        }
                    }
                }
        stage('Container build') {
            steps {
                dir("./testserver") {
                    sh 'docker stop backend || true && docker rm backend || true'
                    sh 'docker rmi backend || true'
                    sh 'docker build -t backend .'
                }
            }
        }
        stage('back-deploy') {
            steps {
                sh 'docker run -it -d -p 8080:8080 --name backend backend'
            }
        }
    }
}