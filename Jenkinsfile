@Library('Shared')_
pipeline{
    agent { label 'dev-server'}
    
    stages{
        stage("Code clone"){
            steps{
                sh "whoami"
            clone("https://github.com/LondheShubham153/django-notes-app.git","main")
            }
        }
        stage("Code Build"){
            steps{
            dockerbuild("notes-app","latest")
            }
        }
        stage("Push to DockerHub"){
            steps{
                dockerpush("dockerHubCreds","notes-app","latest")
            }
        }
        stage('Deploy') {
            steps {
                echo "This is deploying the code" 
                // Stop and remove existing container if it exists
                sh ''' docker rm -f notes-app || true docker run -d -p 8000:8000 --name notes-app notes-app:latest '''
            } 
        }
        
    }
}
