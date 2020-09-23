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
		KUBECONFIG = '/root/.kube/config'
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

      stage('Code Checkout and build') {
        steps {
                checkout scm
		sh 'mvn clean package'
                echo "current branch: $BRANCH_NAME"
              }
          }
                 
      stage('Build docker master') {
        steps {
		script{
                         def dockerImage= docker.build registry + ":$BUILD_NUMBER"
                         docker.withRegistry( '', registryCredential ) {
                                                                          dockerImage.push()
                              }
			 }
                  }
         }

      stage('Doploy images') {
	steps {
		withCredentials([kubeconfigFile(credentialsId: 'alik8s', variable: 'KUBECONFIG')]) {
 		 sh 'kubectl get pods' 
			}	
		}
	}


    }   
}
