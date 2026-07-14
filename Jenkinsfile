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
                withCredentials([
                    string(credentialsId: 'db-url', variable: 'DB_URL'),
                    usernamePassword(
                        credentialsId: 'db-credentials',
                        usernameVariable: 'DB_USER',
                        passwordVariable: 'DB_PASSWORD'
                    )
                ]) {
                    sh 'docker rm -f vehiculosrest || true'
                    sh '''
                        docker run -d \
                        --name vehiculosrest \
                        -p 9090:8080 \
                        -e SPRING_DATASOURCE_URL="$DB_URL" \
                        -e SPRING_DATASOURCE_USERNAME="$DB_USER" \
                        -e SPRING_DATASOURCE_PASSWORD="$DB_PASSWORD" \
                        vehiculosrest
                    '''
                }
            }
        }
    }
}
