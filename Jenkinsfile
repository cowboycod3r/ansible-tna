#!groovy​

stage 'init: update inventory'
node ('master') {
    build 'tna-ansible-etc'
}

stage 'test: clean VM'
node ('master') {
    echo "stop VM"
    sh (script: "VBoxManage controlvm 'tna-ansible-${env.BRANCH_NAME}' poweroff", returnStatus: true)

    echo "reset VM"
    sh "VBoxManage snapshot 'tna-ansible-${env.BRANCH_NAME}' restore prepared"

    echo "start VM"
    sh "VBoxManage startvm 'tna-ansible-${env.BRANCH_NAME}' --type headless"

    sleep 32
    echo "execute only the testing group"

    /* Colorized Console Log */
    wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {

        /* execute ansible limit to testing */
        ansiblePlaybook(playbook: 'site.yml', inventory: "${env.ANSIBLE_INVENTORY}-${env.BRANCH_NAME}", limit: 'testing', colorized: true)
    }

}

stage 'test: used VM'
node ('master') {
    echo "start"
    echo "execute only the testing group"
}

stage 'deployment'
node ('master') {

    echo "execute all other groups with testing group"

    /* check out current state on the node */
    checkout scm

    /* Colorized Console Log */
    wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {

        /* execute ansible excluding testing */
        ansiblePlaybook(playbook: 'site.yml', inventory: "${env.ANSIBLE_INVENTORY}-${env.BRANCH_NAME}", limit: '!testing', colorized: true)
    }
}
