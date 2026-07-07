pipeline {
    agent any

    stages {
        stage('Construir Imagen Docker') {
            steps {
                script {
                    echo 'Construyendo la imagen con Docker Pipeline'
                    docker.build('hola-mundo-node:latest')
                }
            }
        }

        stage('Ejecutar Contenedor Node.js') {
            steps {
                script {
                    def containerName = "hola-mundo-node-${env.BUILD_NUMBER}"
                    echo "Ejecutando contenedor ${containerName}"
                    docker.image('hola-mundo-node:latest').run("-d --name ${containerName} -p 3000:3000")
                }
            }
        }
    }
}