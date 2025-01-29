pipeline {
    agent any

    environment {
        AWS_SERVER_IP = '34.238.135.85' // Replace with your EC2 instance IP
    }

    stages {
        stage('Cleanup') {
            steps {
                cleanWs()
            }
        }

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

        stage('Deploy to AWS') {
            steps {
                sshagent(['aws-server-key']) {
                    bat """
                    pscp -scp -pw your-ec2-password target/simple-java-app-1.0-SNAPSHOT.jar ubuntu@%AWS_SERVER_IP%:/home/ubuntu/app.jar
                    plink -ssh ubuntu@%AWS_SERVER_IP% -pw your-ec2-password "nohup java -jar /home/ubuntu/app.jar > /home/ubuntu/app.log 2>&1 &"
                    """
                }
            }
        }
    }
}
