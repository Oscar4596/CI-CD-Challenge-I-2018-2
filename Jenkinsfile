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
					echo 'Preparing...'
					//sh 'npm install'                               
					
				}                 
			}        

			stage('Build') {      


				steps {                                 
				echo 'Deleting previous images...'
				sh 'if [ "$(docker ps -lq)" != "" ]; then docker rm -f $(docker ps -lq); fi'
				sh 'if [ "$(docker images ${reg} -q)" != "" ]; then docker rmi -f $(docker images ${reg} -q --no-trunc); fi'
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
					echo 'Deleting previous containers...' 
					sh 'if [ "$(docker ps -lq)" != "" ]; then docker rm -f $(docker ps -lq); fi'
					echo 'Deleting done.'
					echo 'Running new container...'
					sh "docker run -d -p 8000:8000 ${reg}:${env.BUILD_ID}"
					echo 'Done'
					}
				}                 
			}         
		} 
} 
