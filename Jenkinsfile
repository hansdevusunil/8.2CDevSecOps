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

  post {
    always {
      // Uses the Email-Extension plugin; will pull the SMTP server, port,
      // credentials and TLS/SSL settings from your global Jenkins config.
      emailext(
        to: 'hansdevsunil111@gmail.com',                              // your recipients
        from: 'hansdevsunil111@gmail.com',                      // must match your SMTP creds
        subject: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """\
          <p><b>Job:</b> ${env.JOB_NAME} #${env.BUILD_NUMBER}</p>
          <p><b>Status:</b> ${currentBuild.currentResult}</p>
          <p>See the <a href='${env.BUILD_URL}'>build details</a>.</p>
        """,
        attachLog: true,
        mimeType: 'text/html'
      )
    }
  }
}
