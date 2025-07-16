pipeline {
  agent any
  environment {
    ANSIBLE_HOST_KEY_CHECKING = 'False'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Deploy via Ansible') {
      steps {
        sshagent(credentials: ['gce-key']) {
          sh '''
            cd ansible
            ansible-playbook -i inventory.ini deploy.yml
          '''
        }
      }
    }
  }
}
