pipeline {
    agent any
    tools {
        maven "localmaven"
    }
    stages {
        stage('SCM Checkout'){
            steps{
                git 'https://github.com/gopal1409/mavenproject1.git'
            }
        }
        stage('MVN Build'){
            steps{
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('MVN test'){
            steps{
                sh "mvn test"
            }
        }
        stage('test report'){
            when {
                expression {choice == 'one'}
            }
            
            steps{
                
                junit 'target/surefire-reports/*.xml'
            }
        }
        stage('archive'){
            when {
                expression {choice == 'two'}
            }
            
            steps{
               
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
        stage('execute ansible'){
            when {
                expression {choice == 'three'}
            }
            steps{
                
              ansiblePlaybook credentialsId: 'ansiblekey', disableHostKeyChecking: true, inventory: 'dev.inv', playbook: 'tomcat.yml'  
            }
        }
    }
}
