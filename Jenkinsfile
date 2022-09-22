pipeline {
    agent any
    
    stages{
        
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '3018580d-d590-4464-a821-09e5d33639bc', url: 'https://github.com/manishsingh26/FlaskExample.git']]])   
            }
        }
        
        stage("Environment") {
            steps {
                sh '''pip3 install virtualenv
                virtualenv --version
                virtualenv flask_app
                virtualenv -p /usr/bin/python3 flask_app
                . flask_app/bin/activate'''
            }
        }
        
        stage("Build") {
            steps {
                sh 'pip3 install -r requirements.txt'
            }
        }
        
        stage("Deploy") {
            steps {
                git branch: 'main', credentialsId: '3018580d-d590-4464-a821-09e5d33639bc', url: 'https://github.com/manishsingh26/FlaskExample.git'
                sh '''nohup python3 app.py & my.log 2>&1 &
                echo $! > save_pid.txt'''
            }
        }
    }
}