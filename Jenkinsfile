pipeline {
    agent any

    stages {
        stage('Clone repo') {
            steps {
                // Replaced with your specific GitHub repository
                git branch: 'main', url: 'https://github.com/monishgowda045/DevOps-Project-Two-Tier-Flask-App.git'
            }
        }

        stage('Build image') {
            steps {
                // Building the individual flask-app image as per your previous request
                sh 'docker build -t flask-app .'
            }
        }

        stage('Deploy with docker compose') {
            steps {
                // Stopping existing containers if they are running; || true prevents the pipeline from failing if none exist
                sh 'docker compose down || true'
                
                // Starting the multi-tier application in detached mode (-d) 
                // This uses the docker-compose.yml file to orchestrate the Flask and MySQL services
                sh 'docker compose up -d --build'
            }
        }
    }
    
    post {
        success {
            echo 'Deployment successful! Your Two-Tier app is running.'
        }
        failure {
            echo 'Deployment failed. Check the Jenkins console logs for errors.'
        }
    }
}
