pipeline {
  agent {
    label 'gpu'
  }
  options {
    timestamps()
    timeout(time: 2, unit: 'HOURS')
    buildDiscarder(logRotator(numToKeepStr: '50'))
    // Jobs can never recover as the agents are ephemeral, for that reason set the durability to PERFORMANCE_OPTIMIZED
    // https://jenkins.io/doc/book/pipeline/scaling-pipeline/#what-am-i-giving-up-with-this-durability-setting-trade-off
    durabilityHint('PERFORMANCE_OPTIMIZED')
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
