pipeline {
    agent any
    tools {
        maven 'maven-3.9'
    }
    stages {
        stage('build jar') {
            steps {
                script {
                    echo "Building the application..."
                    sh 'mvn package'
                }
            }
        }
        stage('build image') {
            steps {
                script {
                    echo "Building the application..."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]){
                        sh 'docker build -t turalasgar/demo-app:jma-4.0 .'
                        sh 'echo $PASS | docker login -u $USER --password-stdin'
                        sh 'docker push turalsagar/demo-app:jma-4.0'
                        sh 'docker rmi turalasgar/demo-app:jma-4.0'
                    }
                }
            }
        }
        stage('test') {
            steps {
                script {
                    echo "Testing the application..."
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo "Deploying the application..."
                }
            }
        }
    }
}
