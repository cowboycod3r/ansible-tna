pipeline {
    agent any
    stages {
        stage('available') {
            steps {
                sh "ansible-playbook site.yml -t 'available'"
            }
        }
        stage('deployment') {
            when {
                expression {
                    branch 'master'
                }
            }
            steps {
                sh "ansible-playbook site.yml -t 'available,deploy'"
            }
        }
        stage('update') {
            steps {
                sh "ansible-playbook site.yml -t 'update'"
            }

        }
    }
}
