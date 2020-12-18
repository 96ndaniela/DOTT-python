pipeline {
    agent any
    environment {
                //script {
                   // withCredentials([string(credentialsId: 'MyOrganization', variable: 'ORGANIZATION')])
                //}
        SCANNER_HOME = tool 'MySQScanner'
   	        //ORGANIZATION = "victor1795"
    	        //PROJECT_NAME = "Victor1795_DOTT-python"
    }
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
 	   
            steps {
		script {
			withCredentials([string(credentialsId: 'MyOrganization', variable: 'ORGANIZATION'), string(credentialsId: 'ProjectKey', variable: 'PROJECT_NAME')]) {
		            //def ORGANIZATION = env.mysecret
			
	                  withSonarQubeEnv('MySQServer') {
	                    sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
                            -Dsonar.java.binaries=build/classes/java/ \
                            -Dsonar.projectKey=$PROJECT_NAME \
                            -Dsonar.sources=.'''
		          }
                       }
                }  
                
            }
        }
        stage('Unit Test') {
            steps {
		script {
		   // try {
			
			//sh 'sonar.python.coverage.reportPaths=/var/lib/jenkins/workspace/test/coverage.xml'
			sh 'ls'
			sh 'pwd'
			    
			withCredentials([string(credentialsId: 'MyOrganization', variable: 'ORGANIZATION'), string(credentialsId: 'ProjectKey', variable: 'PROJECT_NAME')]) {
			    sh 'cd $WORKSPACE/'
                            sh 'coverage run -m pytest $WORKSPACE/tests.py -v | coverage report | coverage xml'
			    //sh 'less $WORKSPACE/coverage.xml'
			    withSonarQubeEnv('MySQServer') {
	                       sh '''$SCANNER_HOME/bin/sonar-scanner -Dsonar.organization=$ORGANIZATION \
                               -Dsonar.java.binaries=build/classes/java/ \
                               -Dsonar.projectKey=$PROJECT_NAME \
                               -Dsonar.python.coverage.reportPaths=$WORKSPACE/coverage.xml'''
			    }
			}
                  //  }
                    //catch (err) {
                      //  echo err.getMessage()
                    //}
		}
	        echo currentBuild.result
	    }
        }	    
        stage('Hello1') {
            steps {
		script {
                    environment {
                        TARGET_CONTAINERID = 'sudo docker ps | grep ash | awk '{ print $1 }''
                    }
	            //try {
			echo $TARGET_CONTAINERID
                        echo 'Hello World'
			//sh 'sudo docker ps | grep ash | awk '{ print $1 }'
			sh 'sudo docker rm -f $TARGET_CONTAINERID'
	                sh 'sudo docker run -d -p 8000:8000 pym'
		    //}
                    //catch (err) {
                      //  echo err.getMessage()
                    //}
		}
	        echo currentBuild.result
            }
        }
    }
}


