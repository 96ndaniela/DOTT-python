pipeline {
    agent any

    stages {
	stage ('Dockerbuild'){
	    steps {
		script {
//	            try {
	                sh 'sudo docker build -t pym .'
//		    }
//		    catch (err) {
//	                echo err.getMessage()
//                    }
		}
//	        echo currentBuild.result
	    }
	}
	stage('SonarCloud') {
            //script {
             //   withCredentials([string(credentialsId: 'MyOrganization', variable: 'ORGANIZATION')])
           // }
 	    environment {
                script {
                    withCredentials([string(credentialsId: 'MyOrganization', variable: 'ORGANIZATION')])
                }
    	        SCANNER_HOME = tool 'MySQScanner'
   	        //ORGANIZATION = "victor1795"
    	        PROJECT_NAME = "Victor1795_DOTT-python"
            }
            steps {
                withSonarQubeEnv('MySQServer') {
                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
                    -Dsonar.java.binaries=build/classes/java/ \
                    -Dsonar.projectKey=$PROJECT_NAME \
                    -Dsonar.sources=.'''
                }
            }
        }
        stage('Unit Test') {
            steps {
		script {
		    try {
                        sh 'pytest tests.py'
                    }
                    catch (err) {
                        echo err.getMessage()
                    }
		}
	        echo currentBuild.result
	    }
        }	    
        stage('Hello1') {
            steps {
                echo 'Hello World'
	        //sh 'sudo docker run -d -p 8000:8000 pym'
            }
        }
    }
}


