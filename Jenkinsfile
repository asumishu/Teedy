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
                sh 'mvn clean install -DskipTests'
            }
        }
        
        stage('PMD Code Check') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }
        
        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }
        
        stage('Generate Test Report') {
            steps {
                sh 'mvn surefire-report:report'
            }
        }
        
        stage('Generate JavaDoc') {
            steps {
                sh 'mvn javadoc:jar'
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
