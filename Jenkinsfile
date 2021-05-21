pipeline {
  agent { docker { image 'python:3.9.4' } }
  stages {
    stage('build') {
      steps {
        sh 'pip install -r requirements.txt'
      }
    }
    stage('test') {
      steps {
        sh 'py.test --junitxml results.xml tests.py'
      }
      post {
        always {
          junit 'test-reports/results.xml'
        }
      }    
    }
  }
}
