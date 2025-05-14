pipeline {
  agent any

  stages {
    stage('Trigger downstream services') {
      parallel {
        stage('microservice1') {
          when {
            changeset "**/microservice1/**"
          }
          steps {
            echo "Changes detected in microservice1/, triggering microservice1-pipeline"
            build job: 'microservice1-pipeline'
          }
        }
        stage('microservice2') {
          when {
            changeset "**/microservice2/**"
          }
          steps {
            echo "Changes detected in microservice2/, triggering microservice2-pipeline"
            build job: 'microservice2-pipeline'
          }
        }
        stage('microservice3') {
          when {
            changeset "**/microservice3/**"
          }
          steps {
            echo "Changes detected in microservice3/, triggering microservice3-pipeline"
            build job: 'microservice3-pipeline'
          }
        }
      }
    }
  }
}
