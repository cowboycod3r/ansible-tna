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
    sh "ansible-playbook site.yml"
    echo "deployment done."
}
