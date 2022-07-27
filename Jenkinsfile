
pipeline {
  agent { label 'Node1' }
  environment {
    imagename = "webapp"
    registryCredential = "docker_registry"
    dockerImage = ''
    }
 
  stages {
    stage('Cloning Git') {
      steps {
        git([url: 'https://github.com/ansil1999/node_appp_ansil.git', branch: 'main'])
 
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }
    stage('Pushing Image') {
      steps{
        script {
          docker.withRegistry('https://www.ansil.tk', 'docker_registry') {
            
             dockerImage.push('latest')
          }
        }
      }
    }
    stage('Deploying Application') {
      steps{
        sh 'docker-compose up -d'
        sh 'docker-compose ps -a'
      }
    }
  }
}
