pipeline
{
  agent any
  triggers {
        pollSCM '* * * * *'
    }
  stages
  {
      stage('Checkout SCM')
      {
          steps
          {
              git 'https://github.com/sureshkumar-devops/sem-project.git'
          }
      }
      stage('Build')
      {
          steps
          {
            sh 'mvn clean package'
          }
          post
          {
              always
              {
                 echo 'Artifacts..packing'
                 archiveArtifacts artifacts: '**/*.war'            
              }
          }
      }
      stage('Create Tomcat Docker Image')
      {
          steps
          {
             sh 'docker build -t --name tomcatsamplewebapp:${env.Build_ID}  . '
          }         
      }
  }
}
