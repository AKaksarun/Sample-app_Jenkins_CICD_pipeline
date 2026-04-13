pipeline {
    agent any

    environment {
        TOMCAT_IP = "172.31.28.95"
        KEY = "jenkinkey.pem"
        PATH = "/usr/bin:/usr/local/bin:/bin:/usr/sbin:/sbin"
    }

    stages {

        stage('Check Tools') {
            steps {
                sh 'echo $PATH'
                sh 'which mvn'
                sh 'mvn -version'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                chmod 400 $KEY
                scp -o StrictHostKeyChecking=no -i $KEY target/sample-app.war ec2-user@$TOMCAT_IP:/opt/tomcat/webapps/
                '''
            }
        }
    }
}
