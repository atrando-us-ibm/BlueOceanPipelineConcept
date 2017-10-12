pipeline {
  agent any
  stages {
    stage('Create New Environment') {
      steps {
        echo 'Creating New Work Environment for User'
        sh '''ssh s27app "pwd; ls -lahF"
ssh s27app \'echo "hello world"\''''
      }
    }
  }
}