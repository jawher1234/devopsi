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



               stage('Docker Build') {
            steps {
               
      	           sh "docker build -t jawher123456/project ."
                
            }
        }


        stage("Login to DockerHub") {
                steps{

                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u jawher123456 -p jawherzr271997'
                }
        }
        stage("Deploy Image to DockerHub") {
                steps{
                    sh 'docker push jawher123456/project'
                }
        }

        
        stage('Start container') {
            steps {
                 sh "docker compose up -d"

            }
        }   

        

         
    }
}
