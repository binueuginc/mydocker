def gv
pipeline {
   agent any
     parameters {
	    choice (name: 'VERSION', choices: ['1.0.1', '1.2.0', '1.3.0'], description: 'Deployment of selected version')
		booleanParam(name: 'executeTest', defaultValue: true, description: '')
	        choice (name: 'BRANCH', choices: ['master', 'prod', 'dev', 'sanity'], description: 'Deployment Git Branch  selected')
		}
         stages {
	    stage('init'){
	     steps {
		   script {
		   gv = load "groovy.script"
		      } 
		   }
	    }
		
	   stage('build') {
	      when {
		     expression {
			     BRANCH_NAME == "${params.BRANCH}" 
				}
			}	
	      steps {
		      script {
			      gv.buildApp()
		      }
		
		  }
		}
		stage('test'){
		   when {
		      expression {
			     params.executeTest == true 
				 }
		   }
		   steps{
		      echo "Testing the application...."
			  
		   }
		}
		stage('deploy'){
		   steps{
		      echo "Deploying the application....."
			 
             }
		}
     }		
}
