pipeline {
  agent any
  environment {
    ANSIBLE_HOST_KEY_CHECKING = 'False'
  }

  stages {
    stage('Checkout') {
      steps {
        // pulls your entire repo
        checkout scm
      }
    }

    stage('Install Ansible') {
      steps {
        sh '''
          # only if Ansible isn’t already on your Jenkins node
          sudo apt update && sudo apt install -y ansible
        '''
      }
    }

    stage('Deploy via Ansible') {
      steps {
        // run your playbook, using the SSH key already on the Jenkins VM
        sh '''
          cd ansible
          ansible-playbook -i inventory.ini deploy.yml \
            --private-key ~/.ssh/id_rsa
        '''
      }
    }
  }
}

