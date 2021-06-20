pipeline {
    agent any
    environment {
        //POSTGRESS_USER = 'postgres'
        //POSTGRESS_PASS = 'root'
        PATH = "/Users/abala/apache-maven-3.6.3/bin:/usr/local/bin:$PATH"
    }

    stages {
         stage('Insanity Tests') {
             steps {
                 echo "Starting Insanity Tests .."
                 sh 'mvn -Dtest=SmokeTest,HttpRequestTest test'
             }
          }

         stage('Unit Tests') {
             steps {
                 echo "Starting Unit Tests .."
                 sh 'mvn -Dtest=UserControllerTest test'
             }
         }

         stage('Build Jar') {
             steps {
                 echo "Building Jar.."
                 echo "Database user is ${POSTGRESS_USER}"
                 echo "Database password is ${POSTGRESS_PASS}"
                 sh 'mvn package -DskipTests'
             }
         }

         stage('Build Docker Image') {
             steps {
                 echo "Building Docker Image.."
                 sh 'docker build -t joeabala/shikateiadminengine .'
             }
         }

         stage('Deploy Image') {
             steps {
                 echo "Deploying Image.."
                 //sh 'docker login -u "joeabala" -p "dockerhub123" docker.io'
                 sh 'docker login -u ${GIT_USER} -p ${GIT_PASSWORD} docker.io'
                 sh 'docker push joeabala/shikateiadminengine'
             }
         }

         stage('SSH') {
             steps {
                 echo "SSH to server.."
                 sh "whoami" // check which user is running docker and allow access to /etc/sudoers
                 sshagent (credentials: ['shikatei-ssh-access']) {
                        //sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker stop shikateiadminengine"
                        //sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker rm shikateiadminengine"
                       // sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker rmi joeabala/shikateiadminengine"
                       // sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker run -p 8089:8090 --name shikateiadminengine --network=shikateinetwork joeabala/shikateiadminengine"
                       //  sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker-compose -f /opt/letsencrypt-docker-nginx/prod/docker-compose.yml down"
                       //sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker-compose -f /opt/letsencrypt-docker-nginx/prod/docker-compose.yml up -d"

                        sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker stop shikateiadminengine"
                        sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker rm shikateiadminengine"
                        sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker rmi joeabala/shikateiadminengine "

                        //sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker-compose -f /opt/letsencrypt-docker-nginx/prod/docker-compose.yml start shikateiadminengine"

                        //sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker run --name shikateiadminengine -p 8089:8088 --network=shikateinetwork joeabala/shikateiadminengine"

                        sh "ssh -vvv -o StrictHostKeyChecking=no -T abala@104.248.81.111 sudo docker-compose -f /opt/letsencrypt-docker-nginx/prod/docker-compose.yml up --detach --build shikateiadminengine"
                 }
             }
         }
                /*stage ('Four') {
                    parallel {
                        stage('Unit Test') {
                            steps {
                                echo "Unit test.."
                            }
                        }
                        stage('Integration Test') {
                            agent {
                                docker {
                                    reuseNode false
                                    image 'joeabala/springbootjenkinskubernetes'
                                }
                            }
                            steps {
                                echo 'Integration tests..'
                            }
                        }
                    }
                }*/
    }
}
