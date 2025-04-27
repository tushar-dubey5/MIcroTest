pipeline {
    agent any

    stages {
        stage('Check Changes') {
            steps {
                script {
                    // Get the list of changed files from the last commit
                    def changedFiles = sh(script: 'git diff --name-only HEAD~1..HEAD', returnStdout: true).trim()
                    echo "Changed files: ${changedFiles}"

                    // Initialize a list to hold triggered jobs
                    def triggeredJobs = []

                    // Trigger specific pipeline based on changed files
                    if (changedFiles.contains('microservice1/')) {
                        if (!triggeredJobs.contains('microservice1-pipeline')) {
                            build job: 'microservice1-pipeline'
                            triggeredJobs.add('microservice1-pipeline')
                        }
                    }
                    if (changedFiles.contains('microservice2/')) {
                        if (!triggeredJobs.contains('microservice2-pipeline')) {
                            build job: 'microservice2-pipeline'
                            triggeredJobs.add('microservice2-pipeline')
                        }
                    }
                    if (changedFiles.contains('microservice3/')) {
                        if (!triggeredJobs.contains('microservice3-pipeline')) {
                            build job: 'microservice3-pipeline'
                            triggeredJobs.add('microservice3-pipeline')
                        }
                    }
                }
            }
        }
    }
}
