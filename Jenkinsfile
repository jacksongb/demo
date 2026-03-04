pipeline {
    agent any
    
    tools {
        maven 'Maven'
        jdk 'JDK17'
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo '📥 拉取代码...'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo '🔨 编译项目...'
                sh 'mvn clean compile'
            }
        }
        
        stage('Test') {
            steps {
                echo '🧪 运行测试...'
                sh 'mvn test'
            }
        }
        
        stage('Package') {
            steps {
                echo '📦 打包...'
                sh 'mvn package -DskipTests'
            }
        }
    }
    
    post {
        success {
            echo '✅ 构建成功！'
        }
        failure {
            echo '❌ 构建失败！'
        }
    }
}
