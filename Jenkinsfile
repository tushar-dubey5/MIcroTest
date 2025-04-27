pipeline {
    agent any
    stages {
        stage('Check Changes') {
            steps {
                script {
                    def changedFiles = sh(script: 'git diff --name-only HEAD~1..HEAD', returnStdout: true).trim()
                    echo "Changed files: ${changedFiles}"
                    
                    if (changedFiles.contains('microservice1/')) {
                        build job: 'microservice1-pipeline'
                    }
                    if (changedFiles.contains('microservice2/')) {
                        build job: 'microservice2-pipeline'
                    }
                    if (changedFiles.contains('microservice3/')) {
                        build job: 'microservice3-pipeline'
                    }
                }
            }
        }
    }
}
