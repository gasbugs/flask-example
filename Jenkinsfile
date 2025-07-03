node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("gasbugs21c/flask-example")
         
     }
     stage('Push image') {
         docker.withRegistry('https://yourdomain.com', 'harbor_cred') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }
}
