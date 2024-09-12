pipeline{
    agent any
    tools{
        mvn "maven-3.9.9"
    }
    stages{
        stage('build') {
            steps {
                script{
                    echo "Building the jar file..."
                    sh 'mvn clean package'
                }
            }
        }

        stage('create image') {
            environment {
                DOCKER_CREDENTIALS = credentials('docker-credentials')
            }
            steps {
                echo "Building the image..."
                withCredentials()
                sh 'docker build -t devops-training:0.1 .'
                sh "echo ${DOCKER_CREDENTIALS_PSW} | docker login -u ${DOCKER_CREDENTIALS_USR} --password-stdin"
                sh 'docker push devops-training:0.1'
            }
        }

        stage('Deploy') {
            steps {
                script {
                    echo "Deploying the app..."
                }
            }
        }
    }
    
}