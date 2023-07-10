pipeline{
    agent any
    stages{
        stage('Clone'){
            steps{
                git branch: 'main', url: 'https://github.com/muppin/django-notes-app'
            }
            
        }
        stage('Build'){
             steps{
                echo "Building the code"
                sh "docker build -t notes-app ."
            }
            
        }
        stage('Push'){
             steps{
                echo "pusing the code to dockerhub"
                withCredentials([usernamePassword(credentialsId: 'muppin', passwordVariable: 'pswd', usernameVariable: 'usr')]) {
                    sh " docker tag notes-app $usr/notes-app:latest "
                    sh " docker login -u $usr -p $pswd"
                    sh " docker push $usr/notes-app:latest"
}
            }
            
        }
        stage('Deploy'){
             steps{
                echo "deploying!!"
                sh " docker-compose down"
                sh " docker-compose up -d"
               
            }
            
        }
    }
}
