pipeline {
    agent any

    stages {
	stage ('Dockerbuild'){
	    steps {
	        sh 'sudo docker build -t pym .'
		sh 'sudo docker run -d -p 8000:8000 pym'
	    }
	}
	stage('SonarCloud') {
 	    environment {
    	        SCANNER_HOME = tool 'MySQScanner'
   	        ORGANIZATION = "victor1795"
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
        stage('Hello1') {
            steps {
                sh 'python tests.py'
            }
        }	    
        stage('Hello1') {
            steps {
                echo 'Hello World'
            }
        }
    }
}

