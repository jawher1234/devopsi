pipeline {
    agent {label "agent"}
 
    stages {
          stage('Git checkout') {
            steps {
                echo "Pulling ...";
                git branch: 'main',
                url:'https://github.com/jawher1234/devopsi.git',
                credentialsId:'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';
                     }
        }

        stage('Maven version'){
            steps {
                sh "mvn -version"
            }
        }

    }
  
}
