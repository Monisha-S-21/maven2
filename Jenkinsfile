pipeline {
    agent any

    tools {
        maven 'sonarmaven'
    }

    environment {
        // SONAR_TOKEN = credentials('maven3') 
        JAVA_HOME = 'C:\\Program Files\\Java\\jdk-17'
        PATH = "${JAVA_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean compile'
            }
        }
        
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }  
      
      
        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the application...'
            }
        }   
        
      stage('SonarQube Analysis') {
    steps {
        // withSonarQubeEnv('SonarQube Scanner') {
        // bat 'gradlew.bat clean build jacocoTestReport'
            bat """
                mvn sonar:sonar \
                -Dsonar.projectKey=maven3 \
                -Dsonar.projectName='maven3' \
                -Dsonar.host.url=http://localhost:9000 \
                -Dsonar.login=sqa_7172fb4913d2fc12a078ba3b6dba6d8f747d5c79 \
                -Dsonar.coverage.jacoco.xmlReportPaths=target/site/jacoco/jacoco.xml
            """
        }
    // }
}

    }
  post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
