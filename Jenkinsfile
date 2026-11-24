pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5000"
        IMAGE_NAME = "anil-demo-app"
    }

    stages {
        stage('Check Docker') {
    steps {
        bat '''
            echo Checking Docker executable...

            "C:\\Users\\STUDENT\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" --version
        '''
    }
}
        stage('1. Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('2. Application Build & Test') {
            steps {
                bat 'python -m py_compile app.py'
            }
        }

        stage('3. Build & Tag Docker Image') {
    steps {
        bat '''
            set "PATH=C:\\Users\\STUDENT\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;%PATH%"

            docker --version

            docker build -t localhost:5000/anil-demo-app:4 -t localhost:5000/anil-demo-app:latest .
        '''
    }
}

        stage('4. Push Image to Registry') {
            steps {
                bat "docker push ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER}"
                bat "docker push ${REGISTRY}/${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        success {
            echo "Pipeline succeeded! Image ${REGISTRY}/${IMAGE_NAME}:${BUILD_NUMBER} is available locally and in the registry."
        }
    }
}
