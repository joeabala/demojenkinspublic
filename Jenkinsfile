pipeline {
    agent any
    environment {
        POSTGRESS_USER = 'postgres'
        POSTGRESS_PASS = 'root'
        //PATH = "/Users/abala/apache-maven-3.6.3/bin:/usr/local/bin:$PATH"
    }

    stages {
         stage('Insanity Tests') {
             steps {
                 echo "Starting Insanity Tests .."
                 sh 'mvn clean'
             }
          }    
    }
}
