pipeline {
    agent any
     
    environment {
        PATH = "/usr/local/maven/bin:$PATH"  // Set Maven's bin directory to the PATH
    }
    stages {
        stage('Build') { 
            steps {
               // sh 'mvn -B -DskipTests clean package'
                 sh 'docker run --rm -v "$HOME/.m2:/root/.m2" -v "$PWD:/app" -w /app maven:3.9.2 mvn -B -DskipTests clean package'
                               
            }
    }
        stage('Test') {
            steps {
                sh 'docker run --rm -v "$HOME/.m2:/root/.m2" -v "$PWD:/app" -w /app maven:3.9.2 mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
      stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }   
    }
}
