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
            scp -o StrictHostKeyChecking=no -r * ec2-user@<EC2_PUBLIC_IP>:/var/www/html/
            ssh -o StrictHostKeyChecking=no ec2-user@<EC2_PUBLIC_IP> 'sudo systemctl restart httpd'
          '''
        }
      }
    }
  }
}
