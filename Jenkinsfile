pipeline { 
	agent any
    stages { 
	    stage('Dev: Clone repository') {
	        steps{
	        	checkout scm
	        }
	    }
        stage('Dev: Build & Test') { 
        	agent {
		        docker {
		            image 'maven:3-alpine'
		            args '-v /root/.m2:/root/.m2'
		        }
   			} 
            steps { 
               sh 'mvn clean package'  
            }
        }    
       	stage('Dev: Build Image') { 
		    steps { 
		    	hello("world")
		       	dockerBuild() 
       		}
       	}
    }
}