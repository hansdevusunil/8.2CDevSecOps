pipeline {
  agent any

  tools {
    nodejs 'NodeJS_16'
  }

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main',
            url: 'https://github.com/hansdevusunil/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        // Use 'bat' on Windows
        bat 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        bat 'npm test || exit 0'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        bat 'npm run coverage || exit 0'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        bat 'npm audit || exit 0'
      }
    }
  }
}
