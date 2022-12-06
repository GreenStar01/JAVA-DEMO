pipeline{
    agent any
    tools{
        Maven  'Maven'
    }
    parameters{
        string( defaultValue: 'Test', name: 'environment')
    }
    stages {

        stage ('GIT Checkout') {
            steps{
                echo 'Checking out source Code from Repo'
                echo "The Environment for Job Execution is ${params.environment}"
                git 'https://github.com/GreenStar01/JAVA-DEMO.git'
            }

        }


        stage ('Pre-build') {
            steps{
                bat 'mvn clean compile'
            }
        }

        stage ('UnitTest'){
            steps{
                bat 'mvn test'
            }
        }

        stage ('Test-Report'){
            steps{
                junit '**/target/surefire-reports/TEST-*.xml'
                jacoco()
            }
        }

        stage ('Build') {
            steps {
                bat 'mvn package '
            }
        }
        stage ('Archive Output'){
            steps{
                archiveArtifacts artifacts: '**/*.war', onlyIfSuccessful: true
            }
        }


    }
}