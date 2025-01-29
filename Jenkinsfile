pipeline {
    agent any
    environment {
        AWS_SERVER_IP = '34.238.135.85'
        AWS_USER = 'ubuntu'
        JAR_NAME = 'demo-0.0.1-SNAPSHOT.jar'
        LOCAL_JAR_PATH = "target\\${JAR_NAME}"
        REMOTE_JAR_PATH = "/home/ubuntu/app.jar"
        LOG_PATH = "/home/ubuntu/app.log"
    }
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
        stage('Deploy to AWS') {
            steps {
                script {
                    def pscpPath = '"C:\\Program Files\\PuTTY\\pscp.exe"' // Adjust if needed
                    def sshPath = '"C:\\Program Files\\PuTTY\\plink.exe"' // Adjust if needed

                    bat """
                        ${pscpPath} -i C:\\path\\to\\your\\aws-private-key.ppk -scp ${LOCAL_JAR_PATH} ${AWS_USER}@${AWS_SERVER_IP}:${REMOTE_JAR_PATH}
                        ${sshPath} -i C:\\path\\to\\your\\aws-private-key.ppk ${AWS_USER}@${AWS_SERVER_IP} "nohup java -jar ${REMOTE_JAR_PATH} > ${LOG_PATH} 2>&1 &"
                    """
                }
            }
        }
    }
}
