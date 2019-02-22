pipeline {
	agent any         
		stages {                 
			stage('Prepare') {                         
				steps {                                 
					echo 'Preparing...'
				}                 
			}                 
			stage('Build') {      


				steps {                                 
				echo 'Deleting previous images...'
				sh '''docker rmi -f $(docker images -q --no-trunc)'''
				echo 'Previous images deleted.'		

					script {
						echo 'Building image...'
					    docker.build "appi:${env.Build_ID}"
						echo 'Image built...'
					}

				}                 
			}                 
			stage('Test') {                         
				steps {                                 
					echo 'Testing...'                        
				}                 
			}
			stage('push') {
				steps {
					echo 'pushing'
				}
			}                 
			stage('Deploy') {                         
				steps {                                 
					echo 'Deploying....'                                     					
				}                 
			}         
		} 
} 
