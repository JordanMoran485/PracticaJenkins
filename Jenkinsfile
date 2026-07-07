pipeline {
    agent any

    stages {
        stage('Verificar acceso a Docker') {
            steps {
                sh '''
                    echo "Comprobando Docker en el agente..."
                    docker --version || { echo "Docker no está disponible en este agente"; exit 1; }
                '''
            }
        }

        stage('Construir Imagen Docker') {
            steps {
                sh 'docker build -t hola-mundo-node:latest .' 
            }
        }

        stage('Ejecutar Contenedor Node.js') {
            steps {
                sh '''
                    docker rm -f hola-mundo-node || true
                    docker run -d --name hola-mundo-node -p 3000:3000 hola-mundo-node:latest
                '''
            }
        }
    }
}