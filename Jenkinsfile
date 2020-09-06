pipeline {
    agent {label 'Node-1'}
    stages {
        stage('Build') {
             agent {
             docker {
              image 'maven:3-alpine'
                args '-v /root/.m2:/root/.m2'
         }
        }
            steps {
                sh 'mvn -B -DskipTests clean package'
                sh 'mvn test'
            } 
             post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
     stage('Test') {
            steps {
                echo 'Mvn Tests done'
            }
        }
        stage('Deliver') {
            steps {
                sh 'chmod +x -R ${WORKSPACE}'
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
