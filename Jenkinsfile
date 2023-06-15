pipeline {
  agent any

  tools {nodejs "NodeJS-18.16.0"}

  stages {
    
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

    stage('Install Python as root') {
      steps {
        sh 'sudo apt-get update && sudo apt-get install -y python3'
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
                echo "deploy to S3 "
                sh 'aws s3 sync .next/ s3://sortlog-frontend-host-bucket'
                }
        }
    }
  }
}
