pipeline {
     environment { 

        registry = "bindu21/test" 

        registryCredential = 'git' 

        dockerImage = '' 

    }
    agent any 
    stages { 
        stage('Cloning our Git') { 

            steps { 
git branch: 'master', credentialsId: '24b97468-f74d-4b0b-8e5d-f3737b8518be', url: 'https://github.com/bindu29/docker.git'
   

            }

        }
       stage('Building our image') { 

            steps { 

                script { 

                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 

                }

            } 

        }
     stage('Deploy our image') { 

            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 

                        dockerImage.push() 

                    }

                } 

            }

        }
        
        stage('Cleaning up') { 

            steps { 

                sh 'docker rmi $(docker images -f "dangling=true" -q)'

            }

        }
}
        
    }
