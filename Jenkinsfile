pipeline {
    agent any

    tools {
        maven 'maven'
        jdk 'jdk11'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean install -DskipTests -B'
            }
        }

        stage('PMD Code Check') {
            steps {
                sh 'mvn pmd:pmd -B'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test -B'
            }
        }

        stage('Generate Test Reports') {
            steps {
                sh 'mvn surefire-report:report -B'
            }
        }

        stage('Generate JavaDoc') {
            steps {
                sh 'mvn javadoc:javadoc -B'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            archiveArtifacts artifacts: '**/target/site/**/*.html', fingerprint: true
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
