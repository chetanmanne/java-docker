pipeline { 

    environment { 

        registry = "chetanmanne/java-docker"

        registryCredential = 'dockerjenkinsintegration' 

        dockerImage = '' 

    }
    agent any 
 tools { 
        maven 'maven-3.9.9'
    }
    stages { 

        stage('Compile and Build Jar') { 

            steps { 

                bat 'mvn clean install'

            }

        } 

        stage('Building our image') { 

            steps { 

                script { 

                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 

                }
            } 
        }

        stage('Deploy our image') { 

            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 

                        dockerImage.push() 

                 }

                } 

            }

        } 

        stage('Cleaning up') { 

            steps { 

                bat "docker rmi ${registry}:${BUILD_NUMBER}" 

            }

        } 

    }

}
