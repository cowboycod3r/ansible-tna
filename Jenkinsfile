#!groovy​

stage 'init: update inventory'
node ('master') {
    build 'tna-ansible-etc'
}

stage 'testing: prepare VM'
node ('master') {

    echo "stop VM"
    sh (script: "VBoxManage controlvm 'tna-ansible-${env.BRANCH_NAME}' poweroff", returnStatus: true)

    echo "reset VM"
    sh "VBoxManage snapshot 'tna-ansible-${env.BRANCH_NAME}' restore prepared"

    echo "start VM"
    sh "VBoxManage startvm 'tna-ansible-${env.BRANCH_NAME}' --type headless"

    sleep 32

}

stage 'testing: clean VM'
node ('master') {

    /* check out current state on the node */
    checkout scm

    /* Colorized Console Log */
    wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {

        /* execute ansible limit to testing */
        ansiblePlaybook(playbook: 'site.yml', inventory: "${env.ANSIBLE_INVENTORY}-${env.BRANCH_NAME}", limit: 'testing', colorized: true)
    }

}

stage 'testing: running VM'
node ('master') {

    /* check out current state on the node */
    checkout scm

    /* Colorized Console Log */
    wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {

        /* execute ansible limit to testing */
        ansiblePlaybook(playbook: 'site.yml', inventory: "${env.ANSIBLE_INVENTORY}-${env.BRANCH_NAME}", limit: 'testing', colorized: true)
    }

}

stage 'testing: stop VM'
node ('master') {

    echo "stop VM"
    sh "VBoxManage controlvm 'tna-ansible-${env.BRANCH_NAME}' poweroff"

}

stage 'deployment'
node ('master') {

    if (env.BRANCH_NAME == 'master') {

        echo "execute all other groups with testing group"

        /* check out current state on the node */
        checkout scm

        /* Colorized Console Log */
        wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {

            /* execute ansible excluding testing */
            ansiblePlaybook(playbook: 'site.yml', inventory: "${env.ANSIBLE_INVENTORY}-${env.BRANCH_NAME}", limit: '!testing', colorized: true)
        }

    } else {
        echo 'no deployment'
    }

}
