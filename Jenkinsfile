pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['staging', 'production'],
            description: 'Select target environment'
        )
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Tests') {
            parallel {

                stage('Unit Tests') {
                    steps {
                        sh 'echo Running Unit Tests'
                    }
                }

                stage('Integration Tests') {
                    steps {
                        sh 'echo Running Integration Tests'
                    }
                }

            }
        }

        stage('Approve') {
            when {
                expression {
                    params.ENVIRONMENT == 'production'
                }
            }
            steps {
                input message: 'Deploy to production?'
            }
        }

        stage('Deploy') {
            steps {
                sh "echo Deploying to ${params.ENVIRONMENT}"
            }
        }

    }

    post {
        always {
            echo 'Pipeline execution completed.'
        }

        success {
            echo 'Build Successful!'
        }

        failure {
            echo 'Build Failed!'
        }
    }
}
