pipeline {
    agent any

    stages {
        stage('Construir Imagen Docker') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker build -t hola-mundo-node:latest .'
                    } else {
                        bat 'docker build -t hola-mundo-node:latest .'
                    }
                }
            }
        }

        stage('Ejecutar Contenedor Node.js') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                            docker stop hola-mundo-node || true
                            docker rm hola-mundo-node || true
                            docker run -d --name hola-mundo-node -p 3000:3000 hola-mundo-node:latest
                        '''
                    } else {
                        bat '''
                            docker stop hola-mundo-node || exit 0
                            docker rm hola-mundo-node || exit 0
                            docker run -d --name hola-mundo-node -p 3000:3000 hola-mundo-node:latest
                        '''
                    }
                }
            }
        }
    }
}