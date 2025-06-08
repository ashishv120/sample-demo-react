pipeline {
    agent any

    environment {
        REACT_DIR = 'frontend'
        BACKEND_DIR = 'backend'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/ashishv120/my-demo-react-proj.git'
            }
        }

        stage('Build React App') {
            steps {
                dir("${REACT_DIR}") {
                    // sh 'npm install'
                    // sh 'npm run build'
                }
            }
        }

        stage('Install Python Deps') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh 'pip3 install -r requirements.txt'
                }
            }
        }

        stage('Run FastAPI') {
            steps {
                dir("${BACKEND_DIR}") {
                    sh 'pkill -f uvicorn || true'
                    sh 'nohup uvicorn main:app --host 0.0.0.0 --port 8000 &'
                }
            }
        }

        stage('Deploy React') {
            steps {
                sh 'sudo cp -r frontend/build/* /var/www/html/'
            }
        }
    }
}

