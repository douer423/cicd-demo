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
                checkout([
                    $class: 'GitSCM', 
                    branches: scm.branches,
                    userRemoteConfigs: [[url: 'https://github.com/douer423/cicd-demo.git']]
                ])
            }
        }

        stage('Build Deploy Code') {
	    steps {
		sh 'echo $env.BRANCH_NAME'
		}
         }
    }   
}
