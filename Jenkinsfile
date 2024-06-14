pipeline {  
    agent any  
    stages {  
            stage ('Git-Checkout') {  
                steps{
                    git credentialsId:  url: 'https://github.com/dkadmin/tomcat-project.git'
                    echo "Checkout successful";
                } 
            }
            stage ('Compile') {  
                  steps{
                    bat label: '', script: 'mvn compile'
                    echo "test successful";
                    
                } 
            }
            stage ('Build') {  
                  steps{
                    bat label: '', script: 'mvn clean'
                    bat label: '', script: 'mvn package'
                    echo "build successful";
                    
                } 
            }
             stage ('Test') {  
                  steps{
                    bat label: '', script: 'mvn test'
                    echo "test successful";
                } 
            }

             post {
                always {
                junit '**/reports/junit/*.xml'
               }
         } 
        stage ('Deploy') {
            steps{
            deploy adapters: [tomcat9(credentialsId: 'tomcatcred', path: '', url: 'http://13.201.71.176	:8080/')], contextPath: 'jenkins_calci', onFailure: false, war: '**/*.war'
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
