pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Compile the code'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Run JUnit and Jest'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Run SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Cloning OWASP NodeGoat for dependency security testing'

                dir('NodeGoat') {
                    git branch: 'master',
                        url: 'https://github.com/OWASP/NodeGoat.git'

                    echo 'Running npm dependency security audit'

                    bat '"C:\\Program Files\\nodejs\\npm.cmd" audit || exit /b 0'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploy to staging server'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Run integration tests on staging'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploy to production server'
            }
        }
    }
}
