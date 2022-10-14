node {
    checkout scm

    docker.withRegistry('registrysfiems.azurecr.io', 'ACR') {

        def customImage = docker.build("my-image:${env.BUILD_ID}")

        customImage.push()
    }
}
