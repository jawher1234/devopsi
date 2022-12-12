pipeline {
    agent any
    
    tools { 
        maven 'Maven 3.6.3'
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                ''' 
            }
        }

        stage ('Build') {
            steps {
                echo 'This is a minimal pipeline.'
            }
        }
        
           stage ('Maven') {
            steps {
                sh 'mvn -version'
            }
        }
        
          stage('Unit Testing'){
            steps{
                sh "mvn test"
            }
        }
        stage ('SRC Analysis Testing SonarQube'){
            steps {

           sh "mvn sonar:sonar -Dsonar.login=admin  -Dsonar.host.url=http://192.168.1.15:9000/ -Dsonar.password=jawher"
            }

         }
          stage('Build Artifact'){
            steps {
                sh 'mvn clean install'
            }

        }
         stage('Compile Project'){
            steps {
                sh 'mvn compile -DskipTests'
            }
        }
                stage("Login to DockerHub") {
                steps{

                    sh 'docker --version'
                }
        }
        
         stage('Nexus') {
        steps {
        sh 'mvn deploy '
      }
    }

         
    }
}