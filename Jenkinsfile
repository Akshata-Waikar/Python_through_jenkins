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
                    sh """#!/bin/bash
ssh -o StrictHostKeyChecking=no \$LIVE_SERVER << 'EOF'
    echo "[1] ✅ Killing any running Flask app..."
    pkill -f flask || echo "Flask not running."

    echo "[2] ✅ Removing old project folder..."
    rm -rf Python_through_jenkins

    echo "[3] ✅ Cloning fresh code..."
    git clone $REPO_URL || { echo "❌ Git clone failed."; exit 1; }

    echo "[4] ✅ Changing directory..."
    cd Python_through_jenkins || { echo "❌ cd failed."; exit 1; }

    echo "[5] ✅ Installing dependencies..."
    pip3 install -r requirements.txt || pip3 install flask || { echo "❌ pip install failed."; exit 1; }

    echo "[6] ✅ Starting Flask app..."
    export FLASK_APP=app.py
    nohup python3 -m flask run --host=0.0.0.0 > flask.log 2>&1 &
    sleep 3

    echo "[7] 📄 Showing log output..."
    tail -n 20 flask.log || echo "❌ Couldn't read log."
EOF
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
