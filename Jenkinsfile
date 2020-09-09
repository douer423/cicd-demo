pipeline {
    agent {
        node {
            label 'master'
        }
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
                    branches: [[name: '*/master']], 
                    userRemoteConfigs: [[url: 'https://github.com/douer423/cicd-demo.git']]
                ])
            }
        }

        //定义mvn环境
        def mvnHome = tool 'Maven'
        env.PATH = "${mvnHome}/bin:${env.PATH}"

        stage('Build Deploy Code') {
            when {
                branch 'master'
            }

            steps {
                sh """
                echo "Building Artifact with Maven"
                """
                sh '/usr/local/apache-maven-3.3.9/bin/mvn package'
            }
        }
    }   
}
