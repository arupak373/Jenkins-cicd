pipeline{

	agent any

	environment {
		DOCKERHUB_CREDENTIALS=credentials('docker-hub-arupak373')
	}

	stages {
	     
	    stage('Code Checkout') {

			steps {
				checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git-rupak', url: 'https://github.com/arupak373/Jenkins-cicd.git']]])
			}
		}

		stage('Build') {

			steps {
				sh 'docker build -t arupak373/firstdemo -f Dockerfile .'
			}
		}

		stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

		stage('Push') {

			steps {
				sh 'sudo docker push arupak373/firstdemo'
			}
		}
	}
	 
		
	post {
		always {
			sh 'docker logout'
		}
	}
		}
	
