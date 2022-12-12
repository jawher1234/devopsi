pipeline {
    agent any
    

    stages {
        
       stage('Git Checkout'){
            
            steps{
                
                script{
                    
                    git branch: 'main', url: 'https://github.com/jawher1234/devopsi.git'
                }
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

        

         
    }
}