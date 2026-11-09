pipeline {
    agent any
    stages
    {
        stage('Build Docker Image') {
            steps {
                echo "Build Docker Image"
                bat "docker build --no-cache -t sample:v1 ." 
            }
        }
        stage('Docker Login') {
            steps {
                  bat 'docker login -u vyshitha -p vyshu@docker'
                }
            }
        stage('push Docker Image to Docker Hub') {
            steps {
                echo "push Docker Image to Docker Hub"
                bat "docker tag sample:v1 vyshitha/exam:latest"               
                    
                bat "docker push vyshitha/exam:latest"
                
            }
        }
        stage('Deploy to Kubernetes') { 
            steps { 
                   
                    bat 'kubectl apply -f deployment.yaml --validate=false' 
                    bat 'kubectl apply -f service.yaml' 
            } 
        }
    }
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}