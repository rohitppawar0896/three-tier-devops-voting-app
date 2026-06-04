pipeline {
    agent any

    stages {

        stage('Checkout Validation') {
            steps {
                echo 'Repository checkout successful'
            }
        }

        stage('Build Vote Image') {
            steps {
                bat 'docker build -t voting-app:%BUILD_NUMBER% app\\vote'
            }
        }

        stage('Build Worker Image') {
            steps {
                bat 'docker build -t worker-app:%BUILD_NUMBER% app\\worker'
            }
        }

        stage('Build Result Image') {
            steps {
                bat 'docker build -t result-app:%BUILD_NUMBER% app\\result'
            }
        }

        stage('Verify Images') {
            steps {
                bat 'docker images'
            }
        }

        stage('Cluster Validation') {
            steps {
                withEnv(["KUBECONFIG=C:\\Users\\Rohit\\.kube\\config"]) {
                    bat 'kubectl get nodes'
                }
            }
        }

        stage('Docker Hub Login') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    bat 'echo %DOCKER_PASS% | docker login -u %DOCKER_USER% --password-stdin'
                }
            }
        }

        stage('Tag Images') {
            steps {
                bat 'docker tag voting-app:%BUILD_NUMBER% sketcherrp/voting-app:%BUILD_NUMBER%'
                bat 'docker tag worker-app:%BUILD_NUMBER% sketcherrp/worker-app:%BUILD_NUMBER%'
                bat 'docker tag result-app:%BUILD_NUMBER% sketcherrp/result-app:%BUILD_NUMBER%'

                bat 'docker tag voting-app:%BUILD_NUMBER% sketcherrp/voting-app:latest'
                bat 'docker tag worker-app:%BUILD_NUMBER% sketcherrp/worker-app:latest'
                bat 'docker tag result-app:%BUILD_NUMBER% sketcherrp/result-app:latest'
            }
        }

        stage('Push Images') {
            steps {
                bat 'docker push sketcherrp/voting-app:%BUILD_NUMBER%'
                bat 'docker push sketcherrp/worker-app:%BUILD_NUMBER%'
                bat 'docker push sketcherrp/result-app:%BUILD_NUMBER%'

                bat 'docker push sketcherrp/voting-app:latest'
                bat 'docker push sketcherrp/worker-app:latest'
                bat 'docker push sketcherrp/result-app:latest'
            }
        }

        stage('Deploy Kubernetes') {
            steps {
                withEnv(["KUBECONFIG=C:\\Users\\Rohit\\.kube\\config"]) {
                    bat 'kubectl apply -f kubernetes'
                    bat 'kubectl rollout status deployment/vote'
                    bat 'kubectl rollout status deployment/worker'
                    bat 'kubectl rollout status deployment/result'
                }
            }
        }

    }
}