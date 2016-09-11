stage 'update inventory'
node {
    echo "execute tna-ansible-etc"
}

stage 'test: clean VM'
node {
    echo "stop, reset, start, execute, stop"
}

stage 'test: existing VM'
node {
    echo "start, execute, stop"
}

stage 'deployment'
node {

    /* check out current state on the node */
    checkout scm

    /* Colorized Console Log */
    wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {

        /* execute ansible */
        ansiblePlaybook(playbook: 'site.yml', inventory: "/etc/ansible/hosts-${env.BRANCH_NAME}", colorized: true)
    }
}
