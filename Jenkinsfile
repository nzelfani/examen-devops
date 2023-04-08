pipeline {
    environment {
        registry = "nour199300/Option2025"
        registryCredential = 'dockerHub'
        dockerImage = ''
    }
    agent any
    stages{
        stage('Clone'){
             steps{  
                 git branch: 'main', url: 'https://github.com/nzelfani/examen-devops.git'
             }
        }  
       stage('MVN CLEAN') {
            steps {
                sh 'mvn clean'
                 
            }
        }
        stage('MVN COMPILE') {
            steps {
                   sh 'mvn compile'
                 
            }
        }
       stage("Unit tests") {
           steps {
                   sh 'mvn test'
             }
             
        }

                stage('Building our image') {
                    steps {
                        script {
                            dockerImage = docker.build registry
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
                    sh "docker rmi $registry"
                    }
                }

    }
}
