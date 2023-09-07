node {
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
        app = docker.build("ghcr.io/imkunyoung/flask-example")
    }
    stage('Push image') {
        docker.withRegistry('https://ghcr.io', 'github_cred') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}
