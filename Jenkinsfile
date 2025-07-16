pipeline {
    agent any

    environment {
        APP_DIR = "Python_through_jenkins"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Akshata-Waikar/Python_through_jenkins'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                    sudo yum install -y python3 mysql
                    curl -O https://bootstrap.pypa.io/get-pip.py
                    sudo python3 get-pip.py
                    sudo pip3 install flask mysql-connector-python
                '''
            }
        }

        stage('Start MariaDB') {
            steps {
                sh '''
                    sudo systemctl start mariadb
                    sudo systemctl enable mariadb
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
