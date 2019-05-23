def label = "worker-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
    containerTemplate(name: 'node', image: 'node:carbon-jessie', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'kubectl', image: 'lachlanevenson/k8s-kubectl:v1.8.8', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'helm', image: 'lachlanevenson/k8s-helm:latest', command: 'cat', ttyEnabled: true)
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

        stage('Create Docker images') {
            container('docker') {
            withCredentials([[$class: 'UsernamePasswordMultiBinding',
            credentialsId: 'dockerhub',
            usernameVariable: 'bvandermeersch',
            passwordVariable: 'Yorkville1!']]) {
            sh """
                docker login -u ${DOCKER_HUB_USER} -p ${DOCKER_HUB_PASSWORD}
                docker build -t namespace/my-image:${gitCommit} .
                docker push namespace/my-image:${gitCommit}
            """
        }
      }
    }
    
    
    }
    }
