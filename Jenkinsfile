stage 'init'
node {
    echo "do something init stuff"
}

stage 'test clean VM'
node {
    echo "test clean VM"
}

stage 'test existing VM'
node {
    echo "test existing VM"
}

stage 'deployment'
node {
    echo "deployment..."
    checkout scm
    ansiblePlaybook(playbook: 'site.yml', inventory: "/etc/ansible/hosts-${env.BRANCH_NAME}")
    echo "deployment done."
}
