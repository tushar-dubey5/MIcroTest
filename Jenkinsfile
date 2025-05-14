pipeline {
    agent any

    stages {
        stage('Determine Changed Services') {
            steps {
                script {
                    // get one path per line
                    def changedFiles = sh(script: 'git diff --name-only HEAD~1..HEAD', returnStdout: true)
                                          .trim()
                                          .readLines()
                    echo "Changed files:\n${changedFiles.join('\n')}"

                    // collect top-level dirs that look like microservices
                    def services = changedFiles.collect { path ->
                        def parts = path.tokenize('/')
                        return parts[0]
                    }.findAll { svc ->
                        svc in ['microservice1','microservice2','microservice3']
                    }.unique()

                    if (services.isEmpty()) {
                        echo "No microservice changes detected; nothing to trigger."
                    } else {
                        services.each { svc ->
                            echo "→ Triggering downstream job for ${svc}"
                            build job: "${svc}-pipeline"
                        }
                    }
                }
            }
        }
    }
}
