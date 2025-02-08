pipeline {
    agent any
     
    environment {
        PATH = "/usr/local/maven/bin:$PATH"  // Set Maven's bin directory to the PATH
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }   
    }
}
