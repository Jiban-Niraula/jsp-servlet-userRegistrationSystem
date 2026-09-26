pipeline {
    agent any
    
    // Defines the tools required. 
    // You must have Maven configured in Jenkins (Manage Jenkins > Tools > Maven Installations).
    tools {
        maven 'Maven 3' // Ensure this matches the name you gave Maven in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                // Automatically pulls the code from your connected GitHub repo
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compiling the Java and Servlet code...'
                // Note: If Jenkins is running on Windows locally, change 'sh' to 'bat'
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Runs JUnit tests if you have them. If they fail, the pipeline stops.
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application into a .war file...'
                sh 'mvn package -DskipTests'
            }
        }

        stage('Archive Artifact') {
            steps {
                echo 'Saving the generated .war file for deployment...'
                // This saves the built .war file in Jenkins so you can download or deploy it
                archiveArtifacts artifacts: 'target/*.war', allowEmptyArchive: false
            }
        }
    }
}
