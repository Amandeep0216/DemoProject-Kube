pipeline{
    agent any

    environment{
        TOMCAT_USER = 'admin'
        TOMCAT_PASS = 'admin'
        TOMCAT_URL = 'http://localhost:9090'
    }
    stages{
        stage('clone repo'){
            steps{
                git 'https://github.com/Amandeep0216/DemoProject-Kube.git'
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
                    def tomcatDeployUrl = "${env.TOMCAT_URL}/manager/text/deploy?path=/simple-java-app&update=true"

                    sh "curl --user ${env.TOMCAT_USER}:${env.TOMCAT_PASS} --upload-file ${warFile} ${tomcatDeployUrl}"
                }
            }
        }
    }
}

