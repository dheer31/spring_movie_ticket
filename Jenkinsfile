node {
    stage('Clone Repo') {
        git 'https://github.com/dheer31/spring_movie_ticket.git'
    }

    stage('Build') {
        sh 'mvn clean package -DskipTests'
    }

    stage('Deploy') {
        sh '''
        pkill -f jar || true
        nohup java -jar target/*.jar > app.log 2>&1 &
        '''
    }
}
