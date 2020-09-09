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
                    userRemoteConfigs: [[url: 'https://github.com/douer423/cicd.git']]
                ])
            }
        }

        stage('Build Deploy Code') {

            when {
                branch 'master'
            }

            steps {

                sh """

                echo "master Building Artifact"

                """

                sh """

                echo "Deploying Code"

                """
            }
        }
    }   
}
