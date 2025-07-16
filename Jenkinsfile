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

