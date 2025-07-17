pipeline {
    agent any

    environment {
        LIVE_SERVER = "ec2-user@43.207.200.231"
        SSH_KEY_ID = "29b37194-4f68-40c3-bb2e-62dee141e2de"
        REPO_URL = "https://github.com/Akshata-Waikar/Python_through_jenkins.git"
    }

    stages {
        stage('Deploy to Live EC2') {
            steps {
                sshagent (credentials: [SSH_KEY_ID]) {
                    sh """
                        ssh -o StrictHostKeyChecking=no $LIVE_SERVER '
                            pkill -f flask || true
                            rm -rf Python_through_jenkins
                            git clone $REPO_URL
                            cd Python_through_jenkins
                            pip3 install -r requirements.txt || pip3 install flask
                            export FLASK_APP=app.py
                            nohup python3 -m flask run --host=0.0.0.0 > flask.log 2>&1 &
                            sleep 3
                            tail -n 10 flask.log
                        '
                    """
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment complete on live server.'
        }
        failure {
            echo '❌ Deployment failed.'
        }
    }
}
