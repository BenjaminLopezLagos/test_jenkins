pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Setup Python Environment') {
            steps {
                sh '''
                   apt install python3.11-venv
                   python3 -m venv venv
                   . venv/bin/activate
                   pip install --upgrade pip
                   pip install pandas scikit-learn joblib
                '''
            }
        }
        stage('Train Model') {
            steps {
                sh '''
                   . venv/bin/activate
                   python train_model.py
                '''
            }
        }
        stage('Validate Model') {
            steps {
                sh '''
                   . venv/bin/activate
                   python validate_model.py
                '''
            }
        }
        stage('Deploy Model') {
            steps {
                sh '''

                   . venv/bin/activate

                   python deploy_model.py

                '''
            }
        }
    }
}

