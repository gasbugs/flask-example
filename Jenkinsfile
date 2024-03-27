node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("admin/flask-example")
         
     }
     stage('Push image') {
         docker.withRegistry('https://127.0.0.1/', 'harbor-reg') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }
     stage('Anchore analyse') {  
           catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS') {
           writeFile file: 'anchore_images', text: '127.0.0.1/admin/flask-example'  
           anchore name: 'anchore_images'  
            }
        }
}
