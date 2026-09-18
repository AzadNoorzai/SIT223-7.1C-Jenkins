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
                echo 'Cloning NodeGoof for dependency security testing'

                dir('nodejs-goof') {
                    git branch: 'main',
                        url: 'https://github.com/snyk-labs/nodejs-goof.git'

                    echo 'Running npm dependency security audit'

                    bat '"C:\\Program Files\\nodejs\\npm.cmd" install || exit /b 0'
                    bat '"C:\\Program Files\\nodejs\\npm.cmd" audit || exit /b 0'
                }
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                echo 'Running SonarCloud code quality and security analysis'

                dir('nodejs-goof') {
                    withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
                        bat '''
                        if not exist sonar-scanner-cli.zip curl.exe -L -o sonar-scanner-cli.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-8.1.0.6389-windows-x64.zip

                        if not exist sonar-scanner-8.1.0.6389-windows-x64 powershell -Command "Expand-Archive -Path sonar-scanner-cli.zip -DestinationPath . -Force"

                        sonar-scanner-8.1.0.6389-windows-x64\\bin\\sonar-scanner.bat ^
                          -Dsonar.projectKey=AzadNoorzai_SIT223-7.1C-Jenkins ^
                          -Dsonar.organization=azadnoorzai ^
                          -Dsonar.host.url=https://sonarcloud.io ^
                          -Dsonar.token=%SONAR_TOKEN% ^
                          -Dsonar.sources=.
                        '''
                    }
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
