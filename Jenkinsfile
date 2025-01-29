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
                dir('demo-webapp') {  // Navigate into the correct subdirectory
                    bat 'mvn clean package'
                    bat 'dir target\\'  // List target directory to verify the JAR file is generated
                }
            }
        }
        stage('Deploy Locally') {
            steps {
                script {
                    bat 'wmic process where "name like \'%%java.exe\' and not CommandLine like \'%%jenkins%%\'" call terminate || echo "No relevant Java process running"'
                    dir('demo-webapp') {  // Navigate to the correct directory
                        bat 'start /b java -jar target/demo-webapp-0.0.1-SNAPSHOT.jar --server.port=8081 > app.log 2>&1'
                    }
                }
            }
        }
    }
}
