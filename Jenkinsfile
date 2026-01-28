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

                    echo "Starting Spring Boot app (fully detached)..."
                    setsid nohup java -jar target/boot-movie-crud-0.0.1-SNAPSHOT.jar \
                      > app.log 2>&1 < /dev/null &

                    sleep 5
                '''
            }
        }
    }

    post {
        success {
            echo "Spring Boot application deployed successfully"
        }
    }
}
