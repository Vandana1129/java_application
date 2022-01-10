pipeline{
    agent any
    
    stages{
        stage('Git Clone'){
            steps{
                git credentialsId: 'my-git-credential', url: 'https://github.com/Vandana1129/java_application.git'
            }
        }
    }
}
