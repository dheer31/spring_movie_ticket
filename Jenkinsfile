pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/sakit333/sak_spring_jenkins_mysql.git'
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

        stage('Deploy to App Server') {
            steps {
                sh '''
                scp target/*.jar ec2-user@<APP_PRIVATE_IP>:/home/ec2-user/
                ssh ec2-user@<APP_PRIVATE_IP> "
                  pkill -f '.jar' || true
                  nohup java -jar /home/ec2-user/*.jar > app.log 2>&1 &
                "
                '''
            }
        }
    }
}
