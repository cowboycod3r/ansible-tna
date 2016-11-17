#!groovy​

stage 'init: update inventory'
node ('master') {
    build 'tna-ansible-etc'
}

stage 'test: clean VM'
node ('master') {
    echo "stop the VM"
    sh (script: "VBoxManage controlvm 'tna-ansible-${env.BRANCH_NAME}' poweroff", returnStatus: true)

    echo "stop, reset, start, execute, stop"
    echo "execute only the testing group"
}

stage 'test: used VM'
node ('master') {
    echo "start, execute, stop"
    echo "execute only the testing group"
}

stage 'deployment'
node ('master') {

    echo "execute all other groups with testing group"

    /* check out current state on the node */
    checkout scm

    /* Colorized Console Log */
    wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {

        /* execute ansible */
        ansiblePlaybook(playbook: 'site.yml', inventory: "${env.ANSIBLE_INVENTORY}-${env.BRANCH_NAME}", colorized: true)
    }
}
