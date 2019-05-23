def label = "worker-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
    containerTemplate(name: 'node', image: 'node:carbon-jessie', command: 'cat', ttyEnabled: true),
]) 
{
    node(label) {
        def commitHash = checkout(scm).GIT_COMMIT    

        stage('Test') {
            container('node') {
            sh """
                pwd
                ls
                npm install
                npm test
                """
            }
        }
    }
    }
