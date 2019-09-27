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
        /*
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarcloud') {
                    sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.6.0.1398:sonar -Dsonar.host.url=$SONAR_HOST_URL  -Dsonar.login=be532c052b2247a704808b6c6b3d4bcdc7a0552d -Dsonar.projectKey=yhippa-dcdojo -Dsonar.organization=yhippa-github'
                }
            }
        }
        stage('Quality Gate') {
            steps {
               timeout(time: 1, unit: 'HOURS') {
                   // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                   // true = set pipeline to UNSTABLE, false = don't
                   waitForQualityGate abortPipeline: true
               }
           }
        }
        stage('upload nexus') {
            steps {
                sh 'mvn deploy'
            }
        }
        */
        stage('build and push docker image') {
            steps {
            // using google JIB plugin                                                                                                                       
            sh 'mvn compile com.google.cloud.tools:jib-maven-plugin:1.3.0:build -DsendCredentialsOverHttp=true'
        }
   }


    }
}
