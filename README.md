# Flask 예제 프로젝트

이것은 간단한 Flask 웹 애플리케이션 예제입니다.

## 프로젝트 구조

```
/
├── Dockerfile
├── Jenkinsfile
├── jenkinsfile_grype
├── jenkinsfile_owasp
├── jenkinsfile_snyk
├── jenkinsfile_sonarqube
├── jenkinsfile_trivy
├── LICENSE
├── README.md
├── requirements.txt
├── test1
├── .git/
├── source/
│   ├── __init__.py
│   ├── app.py
│   └── templates/
│       └── index.html
└── tests/
    ├── __init__.py
    └── test_app.py
```

## 사전 요구 사항

*   Python 3
*   pip
*   Docker (선택 사항)

## 설치

저장소를 복제하고 필요한 Python 패키지를 설치합니다.

```bash
git clone <저장소-url>
cd flask-example
pip install -r requirements.txt
```

## 애플리케이션 실행

### 로컬 환경에서 실행

로컬 머신에서 직접 Flask 애플리케이션을 실행하려면:

```bash
python source/app.py
```

애플리케이션은 `http://localhost:5000`에서 확인할 수 있습니다.

### Docker 사용

Docker를 사용하여 애플리케이션을 빌드하고 실행할 수도 있습니다.

1.  **Docker 이미지 빌드:**

    ```bash
    docker build -t flask-example .
    ```

2.  **Docker 컨테이너 실행:**

    ```bash
    docker run -p 80:80 flask-example
    ```

    애플리케이션은 `http://localhost:80`에서 확인할 수 있습니다.

## 테스트 실행

이 프로젝트는 `pytest`를 사용하여 테스트를 진행합니다. 테스트를 실행하려면:

```bash
pytest
```

## CI/CD

이 프로젝트에는 보안에 중점을 둔 CI/CD 파이프라인을 설정하기 위한 여러 `Jenkinsfile` 구성이 포함되어 있습니다.

*   `Jenkinsfile`: 일반적인 파이프라인 파일입니다.
*   `jenkinsfile_grype`: 취약점 스캐닝을 위해 Grype를 통합합니다.
*   `jenkinsfile_owasp`: OWASP Dependency-Check를 통합합니다.
*   `jenkinsfile_snyk`: 보안 스캐닝을 위해 Snyk를 통합합니다.
*   `jenkinsfile_sonarqube`: 정적 코드 분석을 위해 SonarQube를 통합합니다.
*   `jenkinsfile_trivy`: 취약점 스캐닝을 위해 Trivy를 통합합니다.
