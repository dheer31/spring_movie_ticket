pipeline {
    agent any

    tools {
        maven 'Maven-3.9'
        jdk 'JDK-17'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/your-username/spring-project.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                pkill -f app-name.jar || true
                nohup java -jar target/app-name.jar > app.log 2>&1 &
                '''
            }
        }
    }
} were i need to psate it 
