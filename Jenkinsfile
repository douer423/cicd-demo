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
                        sh '/usr/local/apache-maven-3.3.9/bin/mvn package'
                  }
         }
                 
        stage('Build docker master') {
            when {
                branch 'master' 
               }
                 
            steps {
               script {
           	      docker.withRegistry('https://hub.docker.com/', 'douer423-docker') 

                	def customImage = docker.build("cicd-demo:master")

              		  /* Push the container to the custom Registry */
               		 customImage.push()
                  }
		 }
         }               
    }   
}
