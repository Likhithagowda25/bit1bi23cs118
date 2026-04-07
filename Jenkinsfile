pipeline {
    agent any

    environment {
        JAVA_HOME = "/usr/lib/jvm/java-11-openjdk-amd64"
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    tools {
        maven 'Maven'  // must match the Maven installation name in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Likhithagowda25/bit1bi23cs118.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Run Application') {
            steps {
                sh 'java -jar target/bitMyMavenApp-1.0-SNAPSHOT.jar'
            }
        }
    }

    post {
        success {
            echo 'Build and deployment successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
