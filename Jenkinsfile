pipeline {
    agent any

    tools {
        maven 'M3'
    }

    stages {
        stage('Compilar') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Construir imagen Docker') {
            steps {
                sh 'docker build -t vehiculosrest .'
            }
        }

        stage('Desplegar contenedor') {
            steps {
                sh 'docker rm -f vehiculosrest || true'
                sh 'docker run -d --name vehiculosrest -p 9090:8080 vehiculosrest'
            }
        }
    }
}
