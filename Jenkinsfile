pipeline {
    agent any
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key')   // Replace with your Jenkins credential ID
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key') // Replace with your Jenkins credential ID
        AWS_DEFAULT_REGION = 'us-east-1'  // Replace with your preferred AWS region
    }
    stages {
        stage ('creating setup to k8 cluster')
        {
            steps{
                sh """
                    chmod +x eks.sh
                    ./eks.sh 
                """
            }
        }
        stage ('Login into aws')
        {
            steps {
                    sh '''
                    aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
                    aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
                    aws configure set region $AWS_DEFAULT_REGION
                '''
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