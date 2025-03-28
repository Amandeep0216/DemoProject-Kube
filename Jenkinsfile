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
                echo "Building the project with Maven..."
                sh 'mvn clean package'

                // Debugging: Check if the WAR file is created
                sh 'ls -lh target'
                sh 'jar tf target/simple-java-app.war | grep WEB-INF'

            }
        }

stage('Deploy to Tomcat') {
    steps {
        script {
            def warFile = "target/simple-java-app.war"
            def tomcatWebapps = "/opt/homebrew/Cellar/tomcat/11.0.5/libexec/webapps"

            echo "Deleting old deployment..."
            sh "rm -rf ${tomcatWebapps}/simple-java-app ${tomcatWebapps}/simple-java-app.war"

            echo "Copying new WAR file..."
            sh "cp ${warFile} ${tomcatWebapps}/simple-java-app.war"

            echo "Waiting for Tomcat to deploy the new application..."
            sleep(time:10, unit:"SECONDS") // Give Tomcat some time to deploy

            echo "Application deployed! 🎉 Access it at: http://localhost:9090/simple-java-app/hello"
        }
    }
}
    }
}
