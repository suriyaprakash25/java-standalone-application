pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            // write your logic here
            steps{
            git branch: 'main',
            url: 'https://github.com/expertszen/java-standalone-application.git'
            }
                    
        }
        stage('Build') {
            // write your logic here
            steps{
            bat 'mvn clean compile'
            }
     }
        stage('Run Application') {
            // write your logic here
            steps{
            bat 'mvn package'
            }
        }
        stage('Test') {
            // write your logic here
            steps{
            bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
    post {
    success {
      echo "Build succeeded — triggering downstream job"
      // trigger downstream job; wait:false => don't block. Set wait:true to wait and capture result.
      build job: '2336460-Bhargavi-Munji-java-second-ci-job', wait: false
    }
    failure {
      echo "Build failed — not triggering downstream job"
    }
  }
}
