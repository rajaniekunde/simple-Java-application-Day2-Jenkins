pipeline {
    agent any

    environment {
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-11.0.11' // Update as needed
        PATH = "${JAVA_HOME}\\bin;${env.PATH}"
    }

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
                // Compile all .java files in the src directory recursively
                bat 'javac -d build -sourcepath src src\\main\\java\\**\\*.java'
            }
        }
        
        stage('Run Application') {
            steps {
                echo 'Running the application...'
                // Run the compiled Java application
                bat 'java -cp build Main'
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
