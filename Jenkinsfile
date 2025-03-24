pipeline{
    agent any

    environment{
        TOMCAT_USER = 'admin'
        TOMCAT_PASS = 'admin'
        TOMCAT_URL = 'http://localhost:9090'
    }

    tools {
        maven 'Maven3' // Use the Maven configured in Jenkins
    }
    
    stages{
        stage('clone repo'){
            steps{
                git branch: 'main', url: 'https://github.com/Amandeep0216/DemoProject-Kube.git'
            }
        }
        stage('build with maven'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('Deploy to Tomcat') {
            steps {
                script {
                    def warFile = "target/simple-java-app-1.0.0.war"
                    def tomcatWebapps = "/opt/homebrew/Cellar/tomcat/11.0.5/libexec/webapps"

                    // Ensure the webapps directory exists
                    sh "mkdir -p ${tomcatWebapps}"

                    // Copy WAR file directly for automatic deployment
                    sh "cp ${warFile} ${tomcatWebapps}/simple-java-app.war"
            
                }
            }
        }
    }
}

