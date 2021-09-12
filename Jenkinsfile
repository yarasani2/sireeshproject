pipeline{
    agent any
    environment{
       PATH = "/opt/maven/bin:$PATH"
     }
     stages{
        stage("Git Checkout"){
            steps{
               git branch: 'main', credentialsId: 'gitpassword', url: 'https://github.com/yarasani2/sireeshproject.git'
           }
        }
        stage("Maven Build"){
            steps{
                 sh "mvn clean package"
                 }
         }
        stage("deploy dev"){
            steps{
                sshagent(['']) {
                    sh """   
                    scp -o StrictHostKeyChecking target/*.war srinivas@192.168.0.104:/opt/latest/webapps/
                    ssh srinivas@192.168.0.104 /opt/latest/bin/shutdown.sh
                    ssh srinivas@192.168.0.104 /opt/latest/bin/startup.sh

                   """               
           }
           }
        } 
       }
    }
      
