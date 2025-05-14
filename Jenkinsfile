pipeline {
  agent any
  stages {
    stage('Trigger First Matched Service') {
      steps {
        script {
          def changedFiles = sh(script: 'git diff --name-only HEAD~1..HEAD', returnStdout: true).trim()
          echo "Changed files:\n${changedFiles}"

          if (changedFiles.contains('microservice1/')) {
            echo "Triggering microservice1-pipeline"
            build job: 'microservice1-pipeline'
            return // exit early
          }

          if (changedFiles.contains('microservice2/')) {
            echo "Triggering microservice2-pipeline"
            build job: 'microservice2-pipeline'
            return // exit early
          }

          if (changedFiles.contains('microservice3/')) {
            echo "Triggering microservice3-pipeline"
            build job: 'microservice3-pipeline'
            return // exit early
          }

          echo "No microservice changes detected."
        }
      }
    }
  }
}
