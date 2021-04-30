pipeline {

agent any
environment {
                  hostname = "$hostname"
                  
              }
stages{


    stage('git') {
        steps{
               checkout([
                    $class: 'GitSCM', 
                    branches: [[name: '*/main']], 
                    userRemoteConfigs: [[url: '']]
                ])
        }
}

 stage ('initial') {
             environment {
                  database = DB
              }
              when{
                expression {returns.params == 'Test'|| returns.params == 'UAT' || returns.params == 'Demo' || returns.params == 'Prod'   }
              }
             
              steps{
                  sh  "echo $hostname"
                  sh  "test$DB"


              }
          }


          stage ('build') {
              when { environment name: 'env', value: 'Test' }
              
              steps{

                  git clone https://github.com/devops-34/24aprul
                  git branch: 'feature', changelog: false, poll: false, url: 'https://github.com/devops-34/24aprul'

              }  
}


}
