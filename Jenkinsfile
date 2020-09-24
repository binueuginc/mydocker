pipeline {
  agent any 
	environment {
           NEW_VERSION = '1.0.3'
	   //SERVER_CREDENTIALS = credentials('server-credentials')
	}
    stages {
	   stage('build') {
	      when {
		     expression {
			    BRANCH_NAME == 'master' 
				}
			}	
	      steps {
		    echo "Building the application....."
			echo "Building the application version ${NEW_VERSION}" 
		  }
		}
		stage('test'){
		   when {
		      expression {
			     BRANCH_NAME == 'master' || BRANCH_NAME == 'dev'
				 }
		   }
		   steps{
		      echo "Testing the application...."
			  echo "Testing new application ${NEW_VERSION}"
		   }
		}
		stage('deploy'){
		   steps{
		      echo "Deploying the application....."
			  echo "Deploying the application ${NEW_VERSION}"
			   //echo "Deploying with credentials ${SERVER_CREDENTIALS}"
			   withCredentials([
				   usernamePassword(credentialsId: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)
				   ]) {
					   sh "sshpass ${PWD} ssh -o StrictHostKeyChecking=no ${USER}@192.168.115.244"
				   }
		   }
		}
    }
}	
