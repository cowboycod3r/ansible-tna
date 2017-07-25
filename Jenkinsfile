pipeline {
    agent any
    stages {
        stage('deployment') {
            when {
                expression {
                    branch 'master'
                }
            }
            steps {

                sh "ansible-playbook site.yml -i ${ANSIBLE_INVENTORY} -t 'available'"
            }
        }
    }
}
