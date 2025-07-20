pipeline {
    agent any
   
    stages {
        stage('Create  directory for the WEB Application')
        {
            steps{
               
                //Fisrt, drop the directory if exists
                sh 'rm -rf /home/oarauz/tomcat-web'
                //Create the directory
                sh 'mkdir /home/oarauz/tomcat-web'
                
            }
        }
        stage('Drop the Apache Tomcat Docker container'){
            steps {
            echo 'droping the container...'
            sh 'docker rm -f tomcat1'
            }
        }
        stage('Create the Tomcat container') {
            steps {
            echo 'Creating the container...'
            sh 'docker run -dit --name tomcat1 -p 9090:8080  -v /home/oarauz/tomcat-web:/usr/local/tomcat/webapps tomcat:9.0'
            }
        }
        stage('Copy the web application to the container directory') {
            steps {
                echo 'Creating the shopping folder in the container'
                sh 'mkdir /home/oarauz/tomcat-web/shopping'
                echo 'Copying web application...'             
                sh 'cp -r shopping/* /home/oarauz/tomcat-web/shopping'
            }
        }
    }

    post {
        always{
            echo "This steps always executed"
            cleanWs()
        }
        success {
        // One or more steps need to be included within each condition's block.
        echo 'the deployment has worked'
       }
       failure {
        // One or more steps need to be included within each condition's block.
        echo 'An error has ocurred'
      }
 }
}
