pipeline {
    agent any
    tools {
        maven 'maven3.6.1';
        jdk 'jdk8';
    }
    stages {
        stage('build') {
            steps {
                sh 'mvn clean install'
            }
            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarcloud') {
                    sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar -Dsonar.host.url=$SONAR_HOST_URL  -Dsonar.login=be532c052b2247a704808b6c6b3d4bcdc7a0552d -Dsonar.projectKey=dcdojo -Dsonar.organization=yhippa-github'
                }
            }
        }
        stage('upload nexus') {
            steps {
                sh 'mvn deploy'
            }
        }
    }
}