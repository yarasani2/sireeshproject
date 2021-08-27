node{
      stage("Git Checkout") {
                    git 'https://github.com/yarasani2/sireeshproject.git'
                }
      stage('Compile-Package-create-war-file'){
                 def mvnHome =  tool name: 'maven-3', type: 'maven'
                 bat "${mvnHome}/bin/mvn package"
                    }   
             stage("deploy"){
                steps{
                     sshagent(['tomcat-new']) {
                        sh """
                          scp -o StricktHostKeyChecking=no target/myweb.war ansiadm@192.168.0.109:/opt/apache-tomcat-8.5.70/webapps/
                       """
                 }      
             }
           }
        }
}
