pipeline {
	agent any         
		stages {                 
			stage('Prepare') {                         
				steps {                                 
					git branch: 'Dev', url: 'https://github.com/Oscar4596/CI-CD-Challenge-I-2018-2.git'
				}                 
			}                 
			stage('Build') {                         
				steps {                                 
					echo 'Building..'                         
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
