@Library("praclib") _
pipeline {
    agent { label "agent-1" } 
    stages { 
        stage('Code') {
            steps { 
                script{
                    giturl("https://github.com/KaranGoyal134/django-notes-app.git","main")
                }
            } 
        }
        stage('Push to docker hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: '7d1f564d-30fb-4d22-98cb-bfe8daefbf72',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]){
                sh "docker login -u ${env.DOCKER_USER} -p ${env.DOCKER_PASS}" 
                sh "docker image tag notes-app:latest ${env.DOCKER_USER}/notes-app:latest" 
                sh "docker push ${env.DOCKER_USER}/notes-app:latest" 
                }
            }
        } 
        stage('Deploy') {
            steps {
                sh "docker-compose up -d" 
            }
        }
    }
}
