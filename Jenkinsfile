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
                bat '''
                    if not exist build mkdir build
                    for /r src\\main\\java %f in (*.java) do javac -d build %f
                '''
            }
        }

        stage('Run Application') {
            steps {
                echo 'Running the application...'
                bat '''
                    cd build
                    java Main
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
