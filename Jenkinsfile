pipeline {
  agent {
    label 'gpu'
  }
  options {
    timestamps()
    timeout(time: 2, unit: 'HOURS')
    buildDiscarder(logRotator(numToKeepStr: '50'))
  }
  stages {
    stage('Tensorflow') {
      steps {
        sh """
          source activate tensorflow_p36
          echo "run tensorflow here"
        """
      }
    }
  }
}
