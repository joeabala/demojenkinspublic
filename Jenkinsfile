pipeline {
    agent any
    environment {
        PATH = "/Users/abala/apache-maven-3.6.3/bin:/usr/local/bin:$PATH"
    }

    stages {
         stage('Clone repo') {
             steps {
                 echo "Starting Unit Tests .."
                 sh 'mvn -version'
             }
         }
    }
    
}
