pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/dheer31/spring_movie_ticket.git'
            }
        }

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
                    echo "Stopping old Spring Boot app if running..."
                    pkill -f boot-movie-crud || true

                    echo "Starting Spring Boot app (detached from Jenkins)..."
                    setsid java -jar target/boot-movie-crud-0.0.1-SNAPSHOT.jar \
                      > /var/lib/jenkins/workspace/app/app.log 2>&1 < /dev/null &
                '''
            }
        }
    }

    post {
        success {
            echo "Spring Boot application deployed successfully"
        }
        failure {
            echo "Deployment failed"
        }
    }
}
