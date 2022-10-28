node {
    stage('Docker build e push') {
    checkout scm

    docker.withRegistry('https://registrysfiems.azurecr.io', 'ACR') {

        def customImage = docker.build("my-image:${env.BUILD_ID}")

        customImage.push()
        }
    }
    
    stage ('Deploy docker remoto') {
        
        def dockerRun = 'docker container run -d -p 9005:80 registrysfiems.azurecr.io/my-image:12'
        def dockerRm = 'docker container rm -f $(docker container ps -aq)'
        
        sshagent(['jenkins_remotedocker']) {            
            
        sh "ssh -o StrictHostKeyChecking=no cotin@172.16.0.11 ${dockerRm}"
        
        sh "ssh -o StrictHostKeyChecking=no cotin@172.16.0.11 ${dockerRun}"
        
        }
    }
}


