pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                sh '''
                    chmod +x mvnw
                    ./mvnw clean package -DskipTests
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    echo "Stopping old app if running..."
                    pkill -f 'spring_app_sak' || true

                    echo "Starting Spring Boot app..."
                    nohup java -jar target/*.jar > app.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo "Application deployed successfully"
        }
    }
}
