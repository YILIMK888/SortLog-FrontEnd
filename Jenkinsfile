pipeline {
  agent any

  tools {nodejs "NodeJS-18.16.0"}
  
  stages {
    stage('Checkout') {
      steps {
        // Checkout your source code from your version control system (e.g., Git)
        checkout([$class: 'GitSCM',
              branches: [[name: '*/main']], // Specify the branch to checkout
              userRemoteConfigs: [[url: 'https://github.com/YILIMK888/SortLog-FrontEnd.git']]])
      }
    }

    
    stage('Install Dependencies') {
      steps {
        // Install project dependencies using Node.js and npm or yarn
        sh 'yarn install' // or 'npm install'
      }
    }

    stage('Build') {
      steps {
        // Build the Next.js project
        sh 'yarn run build'
      }
    }


    stage('Deploy') {
        steps {
            // Install AWS CLI (if not already installed)
            sh 'pip install awscli --upgrade --user'

            // Set AWS credentials
            withAWS(credentials: 'mk-aws-credentials', region: 'ap-southeast-2') 
            {
                // Deploy to AWS S3
                sh 'aws s3 sync .next/ s3://sortlog-frontend-host-bucket'
                }
        }
    }
  }
}
