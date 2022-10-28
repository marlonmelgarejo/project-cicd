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
        
        sshagent(['jenkins_remotedocker']) {          
                        
        sh "ssh -o StrictHostKeyChecking=no cotin@172.16.0.11 ${dockerRun}"
        
        }
    }
    
    stage ('Docker ls') {
        
        def dockerls = 'docker container ls'
        
        sshagent(['jenkins_remotedocker']) {          
                        
        sh "ssh -o StrictHostKeyChecking=no cotin@172.16.0.11 ${dockerls}"
        }
    }
}
