pipeline {
    agent any

    triggers {
        cron('@daily')
    }

    stages {
        stage('deployment') {
            when {
                expression {
                    branch 'master'
                }
            }
            steps {
                sh "ansible-playbook site.yml"
            }
        }
    }
}
