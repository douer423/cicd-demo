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

#      stage('Code Checkout and build') {
#        steps {
#                checkout scm
#		sh 'mvn clean package'
#                echo "current branch: $BRANCH_NAME"
#              }
#          }
#                 
#      stage('Build docker master') {
#        steps {
#		script{
#                         def dockerImage= docker.build registry + ":$BUILD_NUMBER"
#                         docker.withRegistry( '', registryCredential ) {
#                                                                          dockerImage.push()
#                              }
#			 }
#                  }
#         }

      stage('Doploy images') {
	steps {
		sh "mkdir -p ~/.kube"
		sh "echo ${k8s_config} | base64 -d > ~/.kube.config"
 		sh 'kubectl get pods' 
			}	
		}
	}


    }   
}
