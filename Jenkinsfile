node {
    // 현재 빌드가 대상으로 하는 소스코드 버전이 Jenkins 워크스페이스에 복사
    stage('Clone repository') {
        checkout scm
    }
    // dockerfile을 사용해 이미지 빌드 수행 
    stage('Build image') {
        app = docker.build("admin/flask-example")
    }
    stage('Test') {
        // 빌드된 컨테이너 내부에서 테스트 실행 (예시: pytest)
        // 이때 이때 Jenkins의 워크스페이스(프로젝트 소스코드가 있는 디렉토리)가
        // 컨테이너의 특정 경로(보통 /home/jenkins/workspace/파이프라인명 등)에
        // 볼륨 마운트됩니다.
        app.inside {
            sh '''
                pwd
                pip install -r requirements.txt
                # HTML 리포트 생성
                pytest tests/ --html=report.html --self-contained-html --junitxml=output/report.xml
            '''
        }
    }
    stage('Publish Reports') {
        // HTML 리포트 게시 (HTML Publisher 플러그인 필요)
        publishHTML(target: [
            allowMissing: false,
            alwaysLinkToLastBuild: true,
            keepAll: true,
            reportDir: '.', // report.html이 생성된 경로
            reportFiles: 'report.html',
            reportName: 'Pytest HTML Report'
        ])
        // JUnit XML 리포트 게시 (JUnit 플러그인 필요)
        junit 'report.xml'
    }
    // 테스트가 통과되면 이미지 업로드 수행 
    stage('Push image') {
         docker.withRegistry('https://yourdomain.com', 'harbor_cred') {
             app.push("${env.BUILD_NUMBER}")
             app.push("latest")
         }
    }
}
