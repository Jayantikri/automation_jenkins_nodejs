pipeline {
    agent any
    environment {
 
        DOCKERHUB_CREDENTIALS = credentials('dockerhub_cred')
    }
    
    stages {
        stage('pwd') {
            steps {
                sh 'ls ; pwd'
            }
        }

            stage('build') {
            steps {
                   
                    sh "docker build -t jaya91/my_react-vite-app:1.0.${BUILD_NUMBER}  ." 
                    sh 'docker images'
                
            }
        }
        
        stage('Deploy our image') {
            steps {
                
                    // Login to Docker Hub using credentials
withCredentials([usernamePassword(credentialsId: 'dockerhub_cred', passwordVariable: 'password', usernameVariable: 'username')]) {
    // some block

                    sh "docker login -u $username -p $password"
                    
                    // Push the Docker image to Docker Hub
                    sh "docker push jaya91/my_react-vite-app:1.0.${BUILD_NUMBER}"
                    
                    // Run the Docker container
                    sh "docker rm -f react_app || true" // Remove the container if it exists
                    sh "docker run -itd --name react_app -p 3000:80 jaya91/my_react-vite-app:1.0.${BUILD_NUMBER}"
                }
            }
        }
    }
}
