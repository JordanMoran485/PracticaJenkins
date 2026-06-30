pipeline {
    agent any

    tools {
        nodejs "Node25" // Conservamos Node ya que este sí se instala correctamente
    }

    stages {
        stage('Construir Imagen Docker') {
            steps {
                // Al no declarar dockerTool arriba, usará el 'docker' global de tu sistema
                sh 'docker build -t hola-mundo-node:latest .'
            }
        }

        stage('Ejecutar Contenedor Node.js') {
            steps {
                sh '''
                    # Detener y eliminar cualquier contenedor previo
                    docker stop hola-mundo-node || true
                    docker rm hola-mundo-node || true

                    # Ejecutar el contenedor de la aplicación
                    docker run -d --name hola-mundo-node -p 3000:3000 hola-mundo-node:latest
                '''
            }
        }
    }
}