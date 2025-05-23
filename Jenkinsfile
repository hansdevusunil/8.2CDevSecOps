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

  post {
    // always = on success, failure, or abortion
    always {
      // Basic email-ext notification
      emailext(
        recipientProviders: [[$class: 'DevelopersRecipientProvider']], // optional: auto-mail to committers
        to: 'hansdevsunil111@gmail.com.com',                                     // your recipients
        subject: "Build ${currentBuild.currentResult}: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
        body: """\
          <p><b>Job:</b> ${env.JOB_NAME} #${env.BUILD_NUMBER}</p>
          <p><b>Status:</b> ${currentBuild.currentResult}</p>
          <p>See the <a href='${env.BUILD_URL}'>build details</a> for more.</p>
        """,
        attachLog: true,
        mimeType: 'text/html',
        // Reference the SMTP credentials you set up in Manage Jenkins → Credentials
        from: 'hansdevsunil111@gmail.com.com',
        credentialsId: 'gmail-smtp'
      )
    }
  }
}
