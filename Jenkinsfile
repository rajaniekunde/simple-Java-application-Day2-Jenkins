pipeline {
    agent any

    environment {
        // Set JAVA_HOME if necessary
        JAVA_HOME = '/path/to/your/java' // Modify this to point to your Java installation
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Compile Application') {
            steps {
                echo 'Compiling the Java application...'

                // Ensure build directory exists
                bat 'if not exist build mkdir build'

                // Compile the Java files
                bat 'for /r "src\\main\\java" %%f in (*.java) do javac -d build %%f'
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running the application...'

                // Change to the build directory
                bat 'cd build'

                // Run the application (ensure the Main class is in the correct package or directory)
                bat 'java Main'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
        }
        success {
            echo 'Build and run successful!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
