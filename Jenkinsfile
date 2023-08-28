node {
    def app

    stage ('clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("node-app-with-docker")
    }

    stage('Test image') {
        app.Inside {
            sh 'echo "Tested passed"'
        }
    }

    stage('Push image') {
        docker.withRegistry('https://registry.docker.com', 'docker-hub-credentials') {
            app.push("${env.BUUILD_NUMBER}")
            app.push("latest")
        }
    }
}