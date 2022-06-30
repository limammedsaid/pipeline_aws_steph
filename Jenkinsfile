pipeline {
  agent any
  environment {
    Cred_KRD = crdentials ('KRD')
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
                      sh ('curl -u $Cred_KRD http://192.168.1.200:8080/job/KRDPipeline/build?token=12345678')

            }          
        }

        stage('Tigger CD') {
            steps{
                script{
                    //WARNING -> this is not secure : tokens should not be used as plain text in the source code
                    //WARNING -> Don't forget to allow the use of a static method in a jenkins script (Administrer Jenkins -> In-process Script Approval)
                    def token = hudson.util.Secret.fromString("11617dd1147e4056e835a7bf08d9820508")
                    def handle = triggerRemoteJob(
                        job: 'http://192.168.160.200:8080/job/KRD_Pipeline_multibranche/job/' + env.BRANCH_NAME,
                        auth: TokenAuth(apiToken: token, userName: 'devops'),
                        parameters: 'SABR_MOTEUR_VERSION=1.2.14\nSABR_IHM_VERSION=2.5.34\nSIMULATEUR_VERSION=12.4.23')
                }
            }          
        }
    }
}

