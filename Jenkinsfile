pipeline{
    
    agent any
    
    stages{
        
        stage('code'){
            steps{
                git branch:'master',
                url: 'https://github.com/Rahulr25/two-tier-flask-app.git'
            }
        }
        
        stage('build'){
            steps{
                sh 'docker build -t two-tier-flask-app .'
            }
        }
        
        stage('push to dockerHub'){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerPass",usernameVariable:"dockerUser")]){
                        sh "docker login -u ${env.dockerUser} -p ${env.dockerPass}"
                        sh "docker image tag two-tier-flask-app ${env.dockerUser}/two-tier-flask-app"
                        sh "docker push ${env.dockerUser}/two-tier-flask-app:latest"
                    }
                }
        }

        stage('test'){
            steps{
                sh 'This is test stage'
            }

        }
        
        stage('deploy'){
            steps{
                sh "docker compose up -d --build flask-app"
            }
        }
    }
}
