pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'maven_3' // Assumes you have configured Maven as a tool in Jenkins
        TOMCAT_URL = 'http://localhost:8080' // Update with your Tomcat URL
        TOMCAT_MANAGER_USERNAME = 'tomcat'
        TOMCAT_MANAGER_PASSWORD = 'tomcat'
        WAR_FILE = 'target/mvn-hello-world1.war' // Update with your actual WAR file name
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building with Maven...'
                sh "${MAVEN_HOME}/bin/mvn clean install"
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                echo 'Deploying to Tomcat...'
                script {
                    // Deploy to Tomcat using manager-script API
                    sh "curl --user ${TOMCAT_MANAGER_USERNAME}:${TOMCAT_MANAGER_PASSWORD} --upload-file ${WAR_FILE} ${TOMCAT_URL}/manager/text/deploy?path=/your-app&update=true"
                }
            }
        }
    }

    post {
        success {
            echo "Deployment successful!"
        }
        failure {
            echo "Deployment failed. Please check logs for details."
        }
    }
}
