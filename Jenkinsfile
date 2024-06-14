pipeline {  
    agent any  
    stages {  
        stage ("Git Checkout"){
            steps{
                git credentialsId: 'github', url: 'https://github.com/dkadmin/tomcat-project.git'
            }
        }
            stage ('Compile') {  
                  steps{
                    sh label: '', script: 'mvn compile'
                    echo "test successful";
                    
                } 
            }
            stage ('Build') {  
                  steps{
                    sh label: '', script: 'mvn clean'
                    sh label: '', script: 'mvn package'
                    echo "build successful";
                    
                } 
            }
             stage ('Test') {  
                  steps{
                    bat label: '', script: 'mvn test'
                    echo "test successful";
                } 
            }
        stage ('Deploy') {
            steps{
            deploy adapters: [tomcat9(credentialsId: 'tomcatcred', path: '', url: 'http://13.201.71.176	:8080/')], contextPath: 'simpliearnarfact', onFailure: false, war: '**/*.war'
             echo "Deploy successful";
            }
        }
        stage ('Monitor') { 
           steps{ 
             echo "Now you can monitor!";
           }
        }
    }
}
