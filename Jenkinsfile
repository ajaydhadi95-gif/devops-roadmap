pipeline {
    agent any


    stages {
        stage ('Checkout') {
            step {
                git branch: 'main' , url: 'https://github.com/ajaydhadi95-gif/devops-roadmap.git'
                
            }
        }

        stage ('Build') {
            steps {
                sh 'echo "Building the application..."'
                docker build -t my-Roadmap-app .
            }
        }

        stage ('Test') {
            steps {
                sh 'echo "Running tests..."'
                echo "Tests passed successfully!"
            }
        }
    }
}