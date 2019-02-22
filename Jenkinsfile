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
					docker.build("appsita:$(env.BUILD_ID)")
					//echo env.BUILD_ID
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
