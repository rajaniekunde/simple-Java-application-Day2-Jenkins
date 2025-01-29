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
                sh 'mvn clean package'
            }
        }
        stage('Deploy to AWS') {
            steps {
                sshagent(['aws-server-key']) {
                    sh '''
                    scp -o StrictHostKeyChecking=no target/demo-0.0.1-SNAPSHOT.jar ubuntu@aws-server-ip:/home/ubuntu/app.jar
                    ssh ubuntu@aws-server-ip 'nohup java -jar /home/ubuntu/app.jar > /home/ubuntu/app.log 2>&1 &'
                    '''
                }
            }
        }
    }
}
