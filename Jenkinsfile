pipeline{
   agent {label 'Jenkins-Agent' }
  tools {
    jdk 'Java17'
    maven 'Maven3'
  }
  stages{
      stage("Cleanup Workspace"){
           steps{
                cleanWS()
                }
      }
      stage("Checkout from SCM"){
         steps{
           git branch: 'main', credentialsId: 'github', url: 'https://github.com/nikithagh/register-app.git'
               }
      }
  }
}
