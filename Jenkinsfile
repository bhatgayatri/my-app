pipeline{
	tools{
	maven 'M2_HOME'
		jdk 'JAVA_HOME'
	      }
	agent {
    		node {
	    		label ''
    			}
  		}
	stages{
           stage('Checkout Stage'){
		   steps{
			   cleanWs()
                  git url: 'https://github.com/bhatgayatri/my-app.git'
			   bat 'mvn validate'
                 bat 'mvn clean'
		      
	       	}
          	}
	
    
	  stage('Compile Stage'){
	       steps{
		       bat 'mvn compile'
		       bat 'mvn test-compile'
	       }
             }
		stage('self phase'){
	       steps{
		       bat 'mvn process-test-resources'
	       }
             }
		
          stage('Static Code Analysis Stage'){
	        steps{
	         	bat 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000'
		     }
	 	}
	  stage('Testing Stage'){
	        steps{
		  		bat 'mvn test'
				bat 'mvn surefire:test'
	     	  	        junit 'target/surefire-reports/*.xml'
			      
	      	             }
			}
           stage('Code Coverage Test'){
		  steps{
				bat 'mvn cobertura:cobertura'
			        bat 'mvn site'
			        cobertura coberturaReportFile: 'target/site/cobertura/coverage.xml'
		  }
	   }
		stage('Performance Testing'){
		  	steps{
		           	   bat 'mvn verify'
	                   	}
	           	}
		   stage('Package'){
          		steps{
				bat 'mvn war:war'
			}
		}
		stage('Deploy')
		{
		  steps{
				bat 'mvn deploy'
			}
		}
		
		stage('Functional Testing'){
          		steps{
				bat 'mvn integration-test'
			}
		}
		
   }
}
