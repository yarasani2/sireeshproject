pipeline{
      agent any

      environment{
           PATH = "C:\Users\91996\Downloads\apache-maven-3.8.2-bin\apache-maven-3.8.2\bin:$PATH"

       }
       stages{
           stage("Git Checkout"){
               steps{
                    git branch: 'main', credentialsId: 'ec2abf84-88be-4e75-9ddc-37c7b94d8b00', url: 'https://github.com/yarasani2/sireeshproject.git'
                }
             }
             stage("Maven Build"){
                 steps{
                     sh "mvn clean package"
                     sh "mv target/*.war target/myweb.war"
                  }
              }
           stages("deploy-dev"){
           steps{
                 sshagent(['tomcat-new']) {
                 sh """
                    scp -o StricktHostKeyChecking=no target/myweb.war ansiadm@192.168.0.109:/opt/apache-tomcat-8.5.70/webapps
                    ssh ansiadm@192.168.0.109 /opt/apache-tomcat-8.5.70/bin/shutdown.sh
                    ssh ansiadm@192.168.0.109 /opt/apache-tomcat-8.5.70/bin/startup.sh

                  """
                 }      
             }
           }
          }
         }    