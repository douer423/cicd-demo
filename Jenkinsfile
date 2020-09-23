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
		
    environment {
		registry = "douer423/cicd-demo"
		registryCredential = 'douer423-docker'
                dockerImage = ''
		k8s_config = credentials('jenkins-k8s-config')
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

      stage('Doploy images') {
	steps {
		sh "echo ${k8s_config} > ~/config" 
 		sh 'kubectl get all' 
		sh 'kubectl apply -f ./helloworld.yml'
		sh 'kubectl apply -f ./helloworld-nodeport-service.yml'
			}	
		}
	}


}
