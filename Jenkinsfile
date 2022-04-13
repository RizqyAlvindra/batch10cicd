def secret = 'Server'
def server = 'docker@103.179.57.251'
def directory = 'wayshub-frontend'
def branch = 'main'

pipeline{
    agent any
    stages{
	stage ('docker delete & git pull'){
	    steps{
	        sshagent ([secret]) {
	            sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
	            cd ${directory}
	            docker-compose down
	            docker system prune -f
	            git pull ${branch}
	            exit
	            EOF"""
	         }
	     }
	 }
	 stage ('docker build'){
	     steps{
	         sshagent ([secret]) {
	             sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
	             cd ${directory}
	             docker-compose build
	             exit
	             EOF"""
	          }
	      }
	  }
	  stage ('docker up'){
	      steps{
	          sshagent ([secret]) {
	              sh """ssh -o StrictHostKeyChecking=no ${server} << EOF
	              cd ${directory}
	              docker-compose up -d
	              exit
	              EOF"""
	           }
	       }   
	   }
       }
   }
}
