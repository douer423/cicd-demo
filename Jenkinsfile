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
		sh 'echo 123'
		}
         }
    }   
}
