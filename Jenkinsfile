pipeline {
    agent any
    tools {nodejs}
    stages {
        stage('Build') { 
            steps {
                sh ' apt update'
                sh 'apt install npm'
            }
        }
    }
}

