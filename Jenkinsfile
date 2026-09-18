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
