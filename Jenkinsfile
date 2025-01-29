pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/rajaniekunde/simple-Java-application-Day2-Jenkins.git'
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Deploy Locally') {
            steps {
                script {
                    bat 'taskkill /F /IM java.exe || echo "No Java process running"'
                    bat 'start /b java -jar target/*.jar > app.log 2>&1'
                }
            }
        }
    }
}
