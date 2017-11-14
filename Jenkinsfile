pipeline {
    agent any
    stages {
        stage('available') {
            steps {
                sh "ansible-playbook site.yml -i ${ANSIBLE_INVENTORY} -t 'available'"
            }
        }
        stage('deployment') {
            when {
                expression {
                    branch 'master'
                }
            }
            steps {
                sh "ansible-playbook site.yml -i ${ANSIBLE_INVENTORY} -t 'available,deploy'"
            }
        }
        stage('update') {
            steps {
                sh "ansible-playbook site.yml -i ${ANSIBLE_INVENTORY} -t 'update'"
            }

        }
    }
}
