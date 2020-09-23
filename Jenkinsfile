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
