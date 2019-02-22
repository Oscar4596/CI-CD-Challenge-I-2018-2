def img
pipeline {
	environment {
		redcred = 'dockerhubcred'

	}
	agent any         
		stages {       
			  
			stage('Prepare') {                         
				steps {  
					sh 'npm install'                               
					echo 'Preparing...'
				}                 
			}        

			stage('Build') {      


				steps {                                 
				echo 'Deleting previous images...'
				sh '''
				if [ "$(docker images -q)" != "" ]; then docker rmi -f $(docker images -q --no-trunc); fi
				'''
				echo 'Previous images deleted.'		

					script {
						echo 'Building image...'
					   	img = docker.build "appi:${env.Build_ID}"
						echo 'Image built...'
					}

				}                 
			}                 
			stage('Test') {                         
				steps {               
					echo 'Testing...'
					sh '''npm test'''
					script {
						img.inside {
							sh '''npm test'''
						}
					}

				}                 
			}
			stage('push') {
				steps {
					echo 'pushing'
					script {
						docker.withRegistry('oscarjazzloor/cichallengerepo', redcred) {
							dockerImage.push()
						}
					}
				}
			}                 
			stage('Deploy') {                         
				steps {                                 
					echo 'Deploying....'                                     					
				}                 
			}         
		} 
} 
