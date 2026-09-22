pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Pulling website code...'
                git branch: 'main', credentialsId: 'github-token', url: ' https://github.com/deepubhakuni5-create/labtech1.git
            }
        }

        stage('Build Docker Image') {
            steps {
                powershell """
                    docker build -t Newimage:latest .
                """
            }
        }

        stage('Run Container') {
            steps {
                powershell """
                    docker stop  Newimage>\$null
                    docker rm  Newimage>\$null
                    docker run -d --name deepu -p 5553:80  Newimage:latest
                """
            }
        }
    }

    post {
        success {
            echo "Website running at: http://localhost:7090"
        }
    }
}
