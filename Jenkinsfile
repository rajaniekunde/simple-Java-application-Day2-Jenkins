pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                git branch: 'main', url: 'https://github.com/rajaniekunde/simple-Java-application-Day2-Jenkins.git'
            }
        }

        stage('Compile Application') {
            steps {
                echo 'Compiling the application...'
                sh """
                set -e
                javac App.java
                """
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running the application...'
                sh """
                sudo pkill -f App || true
                nohup java App > app.log 2>&1 &
                """
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Application deployed successfully and running on localhost:80!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
