pipeline {
    agent {
        node {
            label 'master'
        }
    }
    
    tools{
	maven 'Maven'
	jdk 'jdk8'
	}

    stages {
        stage('Cleanup Workspace') {
            steps {
                cleanWs()
                sh """
                echo "Cleaned Up Workspace For Project"
                """
            }
        }

        stage('Code Checkout') {
            steps {
                checkout scm
                echo "current branch: $BRANCH_NAME"
            }
        }

        stage('Build Deploy Code') {
	    steps {
	           if (BRANCH_NAME.startsWith("master/")) {
	        	sh '/usr/local/apache-maven-3.3.9/bin/mvn package'
		    }
                  }
         }
    }   
}
