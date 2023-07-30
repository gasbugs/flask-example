node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("admin/flask-example")
         
     }
     stage('Push image') {
         docker.withRegistry('https://18.209.59.9', 'docker-hub') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }
}

stage('Build image') {
  app = docker.build("gasbugs/flask-example")
}

stage('Push image') {
  docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') 
  {
     app.push("${env.BUILD_NUMBER}")
     app.push("latest")
  }
}

