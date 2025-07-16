pipeline {
    agent any

    environment {
        APP_DIR = "Python_through_jenkins"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Akshata-Waikar/Python_through_jenkins.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    yum install -y python3 mysql || true
                    curl -O https://bootstrap.pypa.io/get-pip.py
                    python3 get-pip.py
                    pip3 install flask mysql-connector-python
                '''
            }
        }

        stage('Start MariaDB') {
            steps {
                sh '''
                    systemctl start mariadb || true
                    systemctl enable mariadb || true
                '''
            }
        }

        stage('Run Flask App') {
            steps {
                sh '''
                    cd $APP_DIR
                    export FLASK_APP=app.py
                    nohup flask run --host=0.0.0.0 --port=5000 > flask.log 2>&1 &
                '''
            }
        }
    }

    post {
        failure {
            echo '❌ Build failed!'
        }
        success {
            echo '✅ Flask app deployed successfully!'
        }
    }
}
