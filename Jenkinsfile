pipeline {
    agent any
    
    tools {
        maven 'Maven'
        jdk 'JDK17'
    }
    
    environment {
        IMAGE_NAME = 'demo-app'
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
        
        stage('Build Image') {
            steps {
                echo '🐳 构建 Docker 镜像...'
                sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
                sh 'docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${IMAGE_NAME}:latest'
            }
        }
    }
    
    post {
        success {
            echo '✅ 全部完成！'
            sh 'docker images ${IMAGE_NAME}'
        }
        failure {
            echo '❌ 构建失败！'
        }
    }
}
