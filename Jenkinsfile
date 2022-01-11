pipeline{
    agent any
    tools{
        maven "Maven"
    }
    stages{
        stage('Git Clone'){
            steps{
                git credentialsId: 'my-git-credential', url: 'https://github.com/Vandana1129/java_application.git'
            }
        }
        
        stage('Maven Build'){
            steps{
                sh 'mvn clean install'
            }
        }
        
        stage('SonarQube Stage'){
            environment {
                scanner = tool 'Sonar'
            }
            steps{
                withSonarQubeEnv('SonarServer') {
                       sh "${scanner}/bin/sonar-scanner -Dsonar.projectKey=java_maven -Dsonar.sources=. -Dsonar.java.binaries=target/classes/com/mycompany/app/ "
                }
            }
        }
        
        stage('Quality Gate'){
            steps{
                waitForQualityGate abortPipeline: true
            }
        }
    }
}
