pipeline {
  agent {
    docker {
      args '-u root -v $HOME/.m2:/root/.m2'
      image 'bitwiseman/training-blueocean-sample'
    }
    
  }
  stages {
    stage('build') {
      steps {
        sh './jenkins/build.sh'
        archiveArtifacts 'target/*.war'
      }
    }
    stage('test') {
      steps {
        parallel(
          "test": {
            sh './jenkins/test-all.sh'
            junit '**/surefire-reports/**/*.xml'
            junit '**/test-results/karma/*.xml'
            
          },
          "Frontend": {
            sh './jenkins/test-frontend.sh'
            junit '**/test-results/karma/*.xml'
            
          },
          "Perform": {
            sh './jenkins/test-performance.sh'
            
          },
          "Static": {
            sh './jenkins/test-static.sh'
            
          }
        )
      }
    }
  }
}