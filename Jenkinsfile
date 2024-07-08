pipeline {
    agent any
    stages {
        stage ('creating setup to k8 cluster')
        {
            steps{
                sh """
                    ./eks.sh 
                """
            }
        }
        stage ('creating  k8 cluster')
        {
            steps{

                sh """
                eksctl create cluster --config-file=eks.yaml
                """
            }
        }

    }
    post {
        always {

            echo "deleting the previosly runned pipeline"
            deleteDir()
        }
    }
 
}