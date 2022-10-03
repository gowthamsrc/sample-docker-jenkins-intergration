pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Build Application') {
            steps {
                sh 'mvn -f pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Create Tomcat docker image') {
            steps {
                sh "docker build -f Dockerfile -t tomcatsamplewebapp:${env.BUILD_ID}"
            }
        }
    }
}