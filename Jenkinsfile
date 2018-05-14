pipeline {
    agent any

    triggers {
        cron('@daily')
        pollSCM('*/20 * * * *')
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
