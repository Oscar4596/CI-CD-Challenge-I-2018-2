def img
pipeline {
	environment {
		redcred = 'dockerhubcred'
		reg = 'oscarjazzloor/cichallengerepo'

	}
	agent any         
		stages {       
			  
			stage('Prepare') {                         
				steps { 
					/*echo 'Installing NodeJS'
					sh 'curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -'
					sh 'sudo apt-get install -y nodejs'
					echo 'NodeJS installed'*/
					echo 'Preparing...'
					sh 'npm install'                               
					
				}                 
			}        

			stage('Build') {      


				steps {                                 
				echo 'Deleting previous images...'
				sh '''
				if [ "$(docker images -q)" != "" ]; then docker rmi -f $(docker images -q --no-trunc); fi'''
				echo 'Previous images deleted.'		

					script {
						echo 'Building image...'
					   	img = docker.build reg+":${env.Build_ID}"
						echo 'Image built...'
					}

				}                 
			}                 
			stage('Test') {                         
				steps {               
					echo 'Testing...'
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
						docker.withRegistry('', redcred) {
							img.push()
						}
					}
				}
			}                 
			stage('Deploy') {                         
				steps {             
					script {    
					input('Deploy?')
					echo 'Deploying....'
					sh "docker run -d -p 8000:8000 ${env.BUILD_ID}"
					}
				}                 
			}         
		} 
} 
