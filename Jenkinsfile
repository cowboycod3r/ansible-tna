stage 'update inventory'
node ('master') {
    build 'tna-ansible-etc'
}

stage 'test: clean VM'
node ('virtualbox') {
    echo "stop, reset, start, execute, stop"
}

stage 'test: existing VM'
node ('virtualbox') {
    echo "start, execute, stop"
}

stage 'deployment'
node {

    /* check out current state on the node */
    checkout scm

    /* Colorized Console Log */
    wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {

        /* execute ansible */
        ansiblePlaybook(playbook: 'site.yml', inventory: "${env.ANSIBLE_INVENTORY}-${env.BRANCH_NAME}", colorized: true)
    }
}
