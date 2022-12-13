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
        
       stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/jawher1234/devopsi.git'
                }
            }
        }

      stage('maven'){
            steps{
                sh "mvn -version"
            }
        }
        
         stage('Build') {
            steps {
                    sh "mvn install"
                    //sh "mvn compile"
            }
        }
   
          stage('Unit Testing'){
            steps{
                sh "docker --version"
            }
        }
        stage ('SRC Analysis Testing SonarQube'){
            steps {

           sh "mvn sonar:sonar -Dsonar.login=admin  -Dsonar.host.url=http://192.168.1.20:9000/ -Dsonar.password=jawher"
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

        

         
    }
}