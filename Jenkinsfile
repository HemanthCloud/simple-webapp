pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/HemanthCloud/simple-webapp.git'
      }
    }
    
    stage('Deploy to EC2') {
      steps {
        sshagent(['jenkins-ec2-key']) {
          sh '''
            scp -o StrictHostKeyChecking=no -r * ec2-user@65.0.76.23:/var/www/html/
            ssh -o StrictHostKeyChecking=no ec2-user@65.0.76.23 'sudo systemctl restart httpd'
          '''
        }
      }
    }
  }
}
