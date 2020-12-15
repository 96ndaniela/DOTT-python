pipeline {
    agent any

    stages {
	stage('SonarCloud') {
 	    environment {
    	        SCANNER_HOME = tool 'MySQScanner'
   	        ORGANIZATION = "victor1795-github"
    	        PROJECT_NAME = "DOTT-python"
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
                echo 'Hello World'
            }
        }
	stage('Hello2') {
	    steps {
		echo 'Hello World'
	    }
	}
	stage('Hello3'){
	    steps {
		echo 'Hello World'
	    }
	}
    }
}

