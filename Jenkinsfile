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

    stage('Check Python Version') {
            steps {
                sh 'python3 --version'
            }
        }


    stage('Deploy') {
        steps {
            
            // Set AWS credentials
            withAWS(credentials: 'mk-aws-credentials', region: 'ap-southeast-2') 
            {
                // Deploy to AWS S3
                echo "deploy to S3 "
                sh 'aws s3 sync . s3://sortlog-frontend-host-bucket'
                }
        }
    }
  }
}
