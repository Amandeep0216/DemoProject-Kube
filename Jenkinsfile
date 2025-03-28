pipeline {
    agent any

    environment {
        TOMCAT_USER = 'admin'
        TOMCAT_PASS = 'admin'
        TOMCAT_URL = 'http://localhost:9090'
    }

    tools {
        maven 'Maven3' // Use the Maven configured in Jenkins
    }

    stages {
        stage('Clone Repo') {
            steps {
                echo "Cloning repository..."
                git branch: 'main', url: 'https://github.com/Amandeep0216/DemoProject-Kube.git'
                echo "Repository cloned successfully."
            }
        }

        stage('Build with Maven') {
            steps {
                echo "Building project with Maven..."
                sh 'mvn clean package'
                echo "Maven build completed successfully."
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                script {
                    def warFile = "target/simple-java-app-1.0.0.war"
                    def tomcatWebapps = "/opt/homebrew/Cellar/tomcat/11.0.5/libexec/webapps"

                    echo "Ensuring webapps directory exists..."
                    sh "mkdir -p ${tomcatWebapps}"
                    
                    echo "Copying WAR file to Tomcat webapps directory..."
                    sh "cp ${warFile} ${tomcatWebapps}/simple-java-app.war"

                    echo "Restarting Tomcat to apply changes..."
                    sh "brew services restart tomcat"

                    echo "Application deployed successfully! 🎉"
                    echo "Access the application at: ${TOMCAT_URL}/simple-java-app/hello"
                }
            }
        }
    }
}
