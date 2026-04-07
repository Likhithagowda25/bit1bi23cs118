pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'JDK'
    }

    environment {
        APP_NAME = 'bitMyMavenApp'
        JAR_FILE = 'target/bitMyMavenApp-1.0-SNAPSHOT.jar'
    }

    triggers {
        // Poll SCM every 2 minutes (optional)
        pollSCM('H/2 * * * *')
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Likhithagowda25/bit1bi23cs118'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Run Application') {
            steps {
                echo 'Starting application in background...'
                sh '''
                    nohup java -jar ${JAR_FILE} > app.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Build, test, and deployment successful!'
        }
        failure {
            echo '❌ Build failed! Check logs.'
        }
        always {
            echo '📌 Pipeline execution completed.'
        }
    }
}
