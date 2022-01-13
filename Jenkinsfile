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
        
        stage('Deploy to s3'){
            steps{
                s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'vandana-devops-training-2', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: false, selectedRegion: 'us-west-1', showDirectlyInBrowser: false, sourceFile: 'target/*.jar', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'S3', userMetadata: []            }
        }
    }
}
