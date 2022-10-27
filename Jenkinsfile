final String docker_host = "ssh://cotin@172.16.0.11"

node {
    checkout scm

    docker.withRegistry('https://registrysfiems.azurecr.io', 'ACR') {

        def customImage = docker.build("my-image:${env.BUILD_ID}")

        customImage.push()
    }
}

node {
    stage("Deploy Producao"){
        withEnv(["DOCKER_HOST=${docker_host}"]) {
            sshagent( credentials: ['jenkins_remotedocker']) {
                sh "docker -h ${prod_docker_host} run -d -p 80:80 my-image:${env.BUILD_ID}"
            }
        }
    }
}
