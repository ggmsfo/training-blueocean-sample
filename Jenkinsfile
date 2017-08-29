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
      }
    }
    stage('test') {
      steps {
        sh './jenkins/test-all.sh'
        junit '**/surefire-reports/**/*.xml'
      }
    }
  }
}