pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your-username/my-app.git'
            }
        }

        stage('Build Backend') {
            steps {
                sh "cd backend && mvn clean package -DskipTests"
            }
        }

        stage('Deploy Backend') {
            steps {
                sh """
                cp backend/target/demo-1.0.0.jar /var/www/my-app/
                nohup java -jar /var/www/my-app/demo-1.0.0.jar > /var/www/my-app/app.log 2>&1 &
                """
            }
        }

        stage('Deploy Frontend') {
            steps {
                sh """
                mkdir -p /var/www/my-app/frontend
                cp -r frontend/* /var/www/my-app/frontend/
                """
            }
        }
    }
}

