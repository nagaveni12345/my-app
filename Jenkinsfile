pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git url: 'https://github.com/nagaveni12345/my-app.git'
            }
        }

        stage('Build Backend') {
            steps {
                dir('backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Deploy Backend') {
            steps {
                sh '''
                    mkdir -p /var/www/my-app

                    if pgrep -f demo-1.0.0.jar; then
                        pkill -f demo-1.0.0.jar
                    fi

                    cp backend/target/demo-1.0.0.jar /var/www/my-app/

                    nohup java -jar /var/www/my-app/demo-1.0.0.jar \
                        > /var/www/my-app/app.log 2>&1 &
                '''
            }
        }

        stage('Deploy Frontend') {
            steps {
                sh '''
                    mkdir -p /var/www/my-app/frontend
                    cp -r frontend/* /var/www/my-app/frontend/
                '''
            }
        }
    }
}
