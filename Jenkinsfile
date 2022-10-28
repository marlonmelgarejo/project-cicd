node {
    stage('Example') {
    checkout scm

    docker.withRegistry('https://registrysfiems.azurecr.io', 'ACR') {

        def customImage = docker.build("my-image:${env.BUILD_ID}")

        customImage.push()
        }
    }
}
