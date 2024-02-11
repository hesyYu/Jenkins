pipeline {
    agent any

    stages {
        stage('Check and Install Python and pip') {
            steps {
                script {
                    // Python 설치 여부 확인 및 설치
                    if (sh(script: 'command -v python3 || true', returnStdout: true).trim() == '') {
                        echo 'Python is not installed. Installing Python...'
                        sh 'sudo apt-get update && sudo apt-get install -y python3'
                    } else {
                        echo 'Python is already installed.'
                    }
                    // pip 설치 여부 확인 및 설치
                    if (sh(script: 'command -v pip3 || true', returnStdout: true).trim() == '') {
                        echo 'pip3 is not installed. Installing pip3...'
                        sh 'sudo apt-get install -y python3-pip'
                    } else {
                        echo 'pip3 is already installed.'
                    }
                }
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    // Flask와 필요한 패키지 설치
                    sh 'pip3 install Flask'
                }
            }
        }

        stage('Run Flask App') {
            steps {
                script {
                    // Flask 애플리케이션 실행
                    sh 'nohup python3 app/app.py > flask_app.log 2>&1 &'
                    echo 'Flask app is running on localhost.'
                }
            }
        }
    }

    post {
        always {
            echo 'Build and Deployment process completed.'
        }
    }
}
