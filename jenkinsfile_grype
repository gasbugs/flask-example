node {
     stage('Clone repository') {
         checkout scm
     }
     stage('Build image') {
         app = docker.build("admin/flask-example")
         
     }
     stage('Push image') {
         docker.withRegistry('https://127.0.0.1/', 'harbor_cred') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
     }
     stage('Scan') {
           // download report template
           sh 'curl -sfL https://gist.githubusercontent.com/vjayajv/2fc83aaa80656f976bb39b447cad362d/raw/74a09bf76f8017001312daf65cb83f1b4f4e10d1/report.tmpl > report.tmpl'
           
           // Scan all vuln levels
           sh 'mkdir -p reports'
           sh 'ls -R .'
           sh 'grype 127.0.0.1/admin/flask-example:latest -o template -t report.tmpl --file reports/grype.html'
           
           publishHTML target : [
               allowMissing: true,
               alwaysLinkToLastBuild: true,
               keepAll: true,
               reportDir: 'reports',
               reportFiles: 'grype.html',
               reportName: 'Grype Scan',
               reportTitles: 'Grype Scan'
           ]
       }
}
