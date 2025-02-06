pipeline {
    agent any

    stages {
        stage('Clean Docker Environment') {
    steps {
        script {
            // Clean up Docker build cache and remove dangling images
            sh 'docker system prune -f'
            sh 'docker rmi $(docker images -f "dangling=true" -q) || true'
        }
    }
}
         stage('List Files') {
            steps {
                sh 'pwd'       // Print current directory
                sh 'ls -lah'   // List all files with details
                sh 'ls -R'     // List all files recursively
            }
        }
        stage('Build') {
            steps {
                sh 'docker build -t test -f Dockerfile .'
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker tag test:latest hari6494/test:latest'
                //sh 'docker push hari6494/test:latest'
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Run the Docker container
                    sh 'docker run -d --name testcontainer -p 9090:8080 -p 9091:8081 test:latest'
                    //docker run -p 8081:80 testapi
                }
            }
        }
    }
}
