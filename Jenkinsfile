node{
      stage("Git Checkout") {
                    git 'https://github.com/yarasani2/sireeshproject.git'
                }
      stage('Compile-Package-create-war-file'){
                 def mvnHome =  tool name: 'maven-3', type: 'maven'
                 bat "${mvnHome}/bin/mvn package"
                    }   
    }         
