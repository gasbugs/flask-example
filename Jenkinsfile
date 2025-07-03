node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("admin/flask-example")
         
     }
     stage('Test') {
        // 컨테이너 내부에서 테스트 실행 (예시: pytest)
        app.inside {
            sh '''
                ls -al
                pip install -r requirements.txt
                sh 'pytest tests/'
               '''
        }
     }
     stage('Push image') {
         docker.withRegistry('https://yourdomain.com', 'harbor_cred') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }
}
