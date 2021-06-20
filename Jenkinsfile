pipeline {
    agent any
    environment {
        
        POSTGRESS_USER = 'postgres'
        POSTGRESS_PASS = 'root'
        POSTGRESS_HOST = 'localhost'
        POSTGRESS_PORT = '5431'
        //PATH = "/Users/abala/apache-maven-3.6.3/bin:/usr/local/bin:$PATH"
    }

    stages {
         stage('Build') {
             steps {
                 echo "Starting Build .."
                 sh 'mvn package'
                 sh 'docker ps'
             }
          }  
    }
}
