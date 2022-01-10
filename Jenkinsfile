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
    }
}
