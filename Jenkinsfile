pipeline {
    agent any

    environment {
        AWS_SERVER_IP = '<aws-server-ip>'
        SSH_KEY_PATH = '/path/to/your/aws/key.pem'
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                git 'https://github.com/rajaniekunde/simple-Java-application-Day2-Jenkins.git'
            }
        }

        stage('Transfer Files to AWS') {
            steps {
                echo 'Transferring files to AWS...'
                sh """
                scp -i ${SSH_KEY_PATH} App.java ec2-user@${AWS_SERVER_IP}:/home/ec2-user/App.java
                """
            }
        }

        stage('Compile Application on AWS') {
            steps {
                echo 'Compiling application on AWS...'
                sh """
                ssh -i ${SSH_KEY_PATH} ec2-user@${AWS_SERVER_IP} << EOF
                sudo yum install -y java-17-openjdk-devel
                javac /home/ec2-user/App.java
                EOF
                """
            }
        }

        stage('Run Application on AWS') {
            steps {
                echo 'Running application on AWS...'
                sh """
                ssh -i ${SSH_KEY_PATH} ec2-user@${AWS_SERVER_IP} << EOF
                sudo pkill -f App || true
                nohup java -cp /home/ec2-user App > /home/ec2-user/app.log 2>&1 &
                EOF
                """
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
