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
              sshagent(credentials: ['tomcat-new'], ignoreMissing: true) {
                    sh """
                    
                    scp -r target/*.war ansiadm@192.168.0.104:/opt/latest/webapps/
                    ssh ansiadm@192.168.0.104 /opt/latest/bin/shutdown.sh
                    ssh ansiadm@192.168.0.104 /opt/latest/bin/startup.sh

                   """               
           }
           }
        } 
       }
    }
      
