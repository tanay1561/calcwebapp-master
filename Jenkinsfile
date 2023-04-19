pipeline {
    agent any
    stages {
        stage('Git Checkout') {
            steps {
                git url: 'https://github.com/tanay1561/calcwebapp-master.git'    
		        echo "Code Checked-out Successfully!!";
            }
        }
        
        stage('Package') {
            steps {
                bat 'mvn package'    
		        echo "Maven Package Goal Executed Successfully!";
            }
        }
        
        stage('JUNit Reports') {
            steps {
                junit 'target/surefire-reports/*.xml'
		        echo "Publishing JUnit reports"
            }
        }
        
        stage('Jacoco Reports') {
            steps {
                jacoco()
                echo "Publishing Jacoco Code Coverage Reports";
            }
        }

        stage('SonarQube analysis') {
            steps {
                // Change this as per your Jenkins Configuration
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn package sonar:sonar'
                }
            }
        }

//        stage("Quality gate") {
//            steps {
//                waitForQualityGate abortPipeline: true
//            }
//        }
        
        stage('Deploy') {
            steps {
                // Copy the built package to the Tomcat webapps directory
                bat 'copy target\\calcwebapp.war "C:\\Program Files\\Apache Software Foundation\\Tomcat 9.0_Tomcat9_server\\webapps\\"'
                echo "Deployment to Tomcat Server Successful!";
            }
        }
    }
	
    post {
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
    }
}
