pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // Especifica la rama aquí
        git credentialsId: 'dev-test', url: 'https://github.com/josealfredore26/dev-ops-test.git', branch: 'main'
      }
    }
    stage('Install Dependencies') {
      steps {
        sh '''
          export PATH=$PATH:/var/lib/jenkins/.local/bin
          pip install -r requirements.txt
          flake8 --version
          pytest --version
        '''
      }
    }
    stage('Lint') {
      steps {
        sh 'flake8 main.py'
      }
    }
    stage('Test') {
      steps {
        sh 'pytest'
      }
    }
    stage('Deploy') {
      steps {
        echo 'Deploying application...'
      }
    }
  }
  post {
    success {
      echo 'Pipeline succeeded'
    }
    failure {
      echo 'Pipeline failed'
    }
  }
}
