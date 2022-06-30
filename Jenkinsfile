pipeline {
  agent any
  environment {
    Cred_KRD = credentials ('Cred_KRD')
      }
    stages {
        stage('Checkout') {
            steps{
                checkout scm
            }
        }
        stage('Quality Test') {
            steps{
                echo "Running Quality tests"
            }
        }
        stage('Unit Test') {
            steps{
                echo "Running Unit tests"
            }
        }
        stage('Security Test') {
            steps{
                echo "Running Security tests"
            }          
        }
        stage('Build') {
            steps{
                echo "Building artifact"
            }          
        }
        stage('Push') {
            steps{
                echo "Storing artifact"
            }          
        }

        stage('PTrigger Sec') {
            steps{
                      sh ('curl -u $Cred_KRD_USR:$Cred_KRD_PSW http://192.168.160.200:8080/job/KRD_Pipeline_multibranche/job/')
                      parameters: 'SABR_MOTEUR_VERSION=1.2.14\nSABR_IHM_VERSION=2.5.34\nSIMULATEUR_VERSION=12.4.23'

            }          
        }

    }
}

