pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Ankitkumar0909/Jenkins-project.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    echo 'Starting build process...'
                    def buildStatus = sh(script: './gradlew build', returnStatus: true)
                    if (buildStatus != 0) {
                        error 'Build failed! Check logs for more details.'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    echo 'Checking if test task exists...'
                    def testTaskExists = sh(script: "./gradlew tasks --all | grep -q 'test'", returnStatus: true) == 0
                    if (testTaskExists) {
                        echo 'Running tests...'
                        def testStatus = sh(script: './gradlew test', returnStatus: true)
                        if (testStatus != 0) {
                            error 'Tests failed! Check logs for more details.'
                        }
                    } else {
                        echo 'No test task found, skipping test stage.'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Add deployment steps here
            }
        }
    }

    post {
        always {
            echo 'Pipeline execution completed!'
        }
        success {
            echo 'Pipeline ran successfully!'
        }
        failure {
            echo 'Pipeline failed! Check error logs.'
        }
    }
}
