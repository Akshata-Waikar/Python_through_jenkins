pipeline {
    agent any

    environment {
        FLASK_APP = "app.py"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Akshata-Waikar/Python_through_jenkins.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                yum install python3 -y
                curl -O https://bootstrap.pypa.io/get-pip.py
                python3 get-pip.py
                pip3 install flask mysql-connector-python
                '''
            }
        }

        stage('Run Flask App') {
            steps {
                sh '''
                export FLASK_APP=app.py
                nohup flask run --host=0.0.0.0 --port=5000 &
                '''
            }
        }
    }
}
