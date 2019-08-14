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
               sh 'mvn -B -DskipTests clean package'  
            }
        }    
       	stage('Dev: Build Image and Push') { 
		    steps { 
		    	script{
		    	    hello("world")
			       	app = dockerBuild() 
			       	withDockerRegistry([credentialsId: 'docker-hub-credentials', url: "https://registry.hub.docker.com"]) {
	            		app.push("latest")
        			}
		    	}		    	
       		}
       	}
    }
}