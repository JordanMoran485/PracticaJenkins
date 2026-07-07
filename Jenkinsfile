pipeline {
    agent any

    stages {
        stage('Verificar Docker') {
            steps {
                script {
                    if (isUnix()) {
                        sh '''
                            if ! command -v docker >/dev/null 2>&1; then
                                echo "ERROR: Docker no está disponible en este agente de Jenkins."
                                echo "Instala Docker en el agente o usa un agente con Docker habilitado."
                                exit 1
                            fi
                            docker --version
                        '''
                    } else {
                        bat '''
                            where docker >nul 2>nul
                            if errorlevel 1 (
                                echo ERROR: Docker no está disponible en este agente de Jenkins.
                                echo Instala Docker en el agente o usa un agente con Docker habilitado.
                                exit /b 1
                            )
                            docker --version
                        '''
                    }
                }
            }
        }

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