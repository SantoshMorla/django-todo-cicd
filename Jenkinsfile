pipeline{
        agent {label 'Dev-Django'}
            stages{
                stage('Code'){
                    steps{
                        git url: 'https://github.com/SantoshMorla/django-todo-cicd.git',branch: 'develop'
                    }
                }
                
                stage('Build and Test'){
                    steps {
                        sh 'docker build . -t devsantosh03/django-app:latest'
                    }
                }
                stage('Logging and Push'){
                    steps {
                        echo"Logging and pushing to DockerHub"
                        
						withCredentials([usernamePassword(credentialsId :'dockerhub',passwordVariable:'dockerhubPassword',usernameVariable:'userName')]){
                            sh "docker login -u ${env.userName} -p ${env.dockerhubPassword}"
                            sh "docker push devsantosh03/django-app:latest"
                            
                        }
                    }
                }
                stage('Deploying'){
                    steps{
                      sh 'docker-compose down && docker-compose up -d' 
                    }
                }
                 
    
            }    
        }
