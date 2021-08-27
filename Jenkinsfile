pipeline{
      agent any
       stages{
           stage("Git Checkout"){
               steps{
                    git branch: 'main', credentialsId: 'ec2abf84-88be-4e75-9ddc-37c7b94d8b00', url: 'https://github.com/yarasani2/sireeshproject.git'
                }
             }
            stage('Compile-Package-create-war-file'){
                  steps{
                 
                       bat "${mvnHome}/bin/mvn package"
                    }   
                 }
             stage("deploy"){
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
