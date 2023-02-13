pipeline {
  agent {slave}
  stages {
      stage("Checking Docker Version") {
          steps {
              retry(3){
              sh "docker --version"
              }
          }
      }
      stage("Checking GIT Version") {
          steps {
              sh "git --version"
          }
      }
      stage('Build Docker Image and pull') {
          steps {
              sh 'docker build -t apacheimage:${BUILD_NUMBER} . '
              sh 'docker images'
              sh "docker pull ${REPOSITORY_URI}:${IMAGE_TAG}"
              sh "docker images"
              sh "docker run -d --name apacheimage${BUILD_NUMBER} ${REPOSITORY_URI}"
              sh "docker ps"
          }
      }
    }
}
