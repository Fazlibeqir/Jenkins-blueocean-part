pipeline {
    agent any  // Runs the pipeline on any available agent

    environment {
        // Optional: Define any environment variables here, if necessary
        DOCKER_IMAGE = 'redbfs/jenkins-blueocean-part'  // Example Docker image name
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm  // Clone the repository from the source control manager
            }
        }

        stage('Build Docker image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile in the repository
                    app = docker.build(DOCKER_IMAGE)
                }
            }
        }

        stage('Push Docker image') {
            steps {
                script {
                    // Push the built Docker image to Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
