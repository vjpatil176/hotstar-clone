pipeline {
    agent any
    tools {
        nodejs 'nodejs'
    }
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('GitClone files') {
            steps {
                git 'https://github.com/vjpatil176/hotstar-clone.git'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh "$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=Hotstarpro -Dsonar.projectName=Hotstarpro "
                }
            }
        }
        stage('S3 Backup') {
            steps {
                sh 'aws s3 cp /var/lib/jenkins/workspace/hotstarpro/ s3://hotstarpro/hotstarpro/ --recursive'
            }
        }
    }
}
