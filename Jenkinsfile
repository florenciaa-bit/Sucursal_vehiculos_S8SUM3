pipeline {
    agent any

    stages {
        stage('Clonar repositorio') {
            steps {
                git 'https://github.com/florenciaa-bit/Sucursal_vehiculos_S8SUM3.git'
            }
        }

        stage('Compilar') {
            steps {
                sh './mvnw clean package -DskipTests'
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
