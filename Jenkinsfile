#!/groovy

def imageName

pipeline {
    agent any
    options {
        timestamps()
        timeout(time: 1, unit: 'HOURS')
    }
    stages {
        stage('Pull code') {
            steps {
                script {
                    sh "git clone https://github.com/aditya-sridhar/simple-reactjs-app.git"
                }
            }
        }
        
        stage('Validate code') {
            steps {
                script {
                    dir("simple-reactjs-app/src") {
                        withCredentials([string(credentialsId: 'sonar-token', variable: 'TOKEN')]) {
                            sh "docker run --rm -v ${pwd()}:/usr/src --link sonarqube newtmitch/sonar-scanner sonar-scanner -Dsonar.login='${TOKEN}' -Dsonar.host.url=http://sonarqube:9000 -Dsonar.jdbc.url=jdbc:h2:tcp://sonarqube/sonar -Dsonar.projectKey=MyProjectKey -Dsonar.projectName='Simple React App' -Dsonar.projectVersion=1 -Dsonar.projectBaseDir=/usr/src -Dsonar.sources=."
                        }
                    }
                }
            }
        }
        
        stage('Build image') {
            steps {
                script {
                    imageName = "react-app"
                    sh "git clone https://github.com/GastonKanze/react-app.git"
                    sh "cp react-app/Dockerfile simple-reactjs-app"
                    dir("simple-reactjs-app") {
                        sh "docker build -t ${imageName}:${BUILD_NUMBER} ."
                    }
                }
            }
        }
        
        stage('Push image') {
            steps {
                script {
                    dockerHubRepo = "gastonkanze/${imageName}"
                    withCredentials([usernamePassword(credentialsId: 'DOCKER-LOGIN', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh "docker login -u ${USERNAME} -p ${PASSWORD}"
                        sh "docker tag ${imageName}:${BUILD_NUMBER} ${dockerHubRepo}:${BUILD_NUMBER}"
                        sh "docker tag ${imageName}:${BUILD_NUMBER} ${dockerHubRepo}:latest"
                        sh "docker push ${dockerHubRepo}:${BUILD_NUMBER}"
                        sh "docker push ${dockerHubRepo}:latest"
                    }
                }
            }
        }
        
        stage('Deploy to K8S') {
            steps {
                script {
                    sh "microk8s.kubectl apply -f react-app/simple-react-app-service.yml"
                    echo "Service is pointing to the IP:"
                    sh "microk8s.kubectl get service/simple-react-app -o jsonpath='{.spec.clusterIP}'"
                }
            }
        }
        
    }

    post {
        cleanup {
            cleanWs()
        }
        success {
            script {
                echo "Build success"
            }
        }
        failure {
            script {
                echo "Build failed"
            }
        }
        unstable {
            script {
                echo "Build unstable"
            }
        }
    }
}
