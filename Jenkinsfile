pipeline {
    agent any
    
    tools {
        maven 'Maven'
        jdk 'JDK'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/asumishu/Teedy.git'
            }
        }
        
        stage('Maven Build') {
            steps {
                bat 'mvn clean install -DskipTests'
            }
        }
        
        stage('PMD Code Check') {
            steps {
                bat 'mvn pmd:pmd'
            }
        }
        
        stage('Run Tests') {
            steps {
                bat 'mvn test -Dmaven.test.failure.ignore=true'
            }
        }
        
        stage('Generate Test Report') {
            steps {
                bat 'mvn surefire-report:report'
            }
        }
        
        stage('Generate JavaDoc') {
            steps {
                bat 'mvn javadoc:jar'
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: '**/target/*.jar, **/target/site/**/*.html', allowEmptyArchive: true
        }
        success {
            echo '构建成功！'
        }
        failure {
            echo '构建失败！'
        }
    }
}
