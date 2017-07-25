#!groovy​

stage 'deployment'
node ('master') {

    if (env.BRANCH_NAME == 'master') {

        /* check out current state on the node */
        checkout scm

        /* Colorized Console Log */
        wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {

            /* execute ansible excluding testing */
            ansiblePlaybook(playbook: 'site.yml', inventory: "${env.ANSIBLE_INVENTORY}",  tags: 'available,deploy', colorized: true)
        }

    } else {
        echo 'no deployment'
    }

}
