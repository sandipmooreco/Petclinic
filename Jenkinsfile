pipeline {
    agent any

    tools { 
        maven 'maven3' 
        jdk 'jdk17' 
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    changelog: false,
                    credentialsId: 'git-login',
                    poll: false,
                    url: 'https://github.com/sandipmooreco/Petclinic.git'
            }
        }

        stage('Clean') {
            steps {
                withMaven(globalMavenSettingsConfig: '',
                          jdk: 'jdk17',
                          maven: 'maven3',
                          mavenSettingsConfig: '',
                          traceability: true) {
                    sh 'mvn clean'
                }
            }
        }

        stage('compile') {
            steps {
                withMaven(globalMavenSettingsConfig: '',
                          jdk: 'jdk17',
                          maven: 'maven3',
                          mavenSettingsConfig: '',
                          traceability: true) {
                    sh 'mvn compile'
                }
            }
        }
        stage('package') {
            steps {
                withMaven(globalMavenSettingsConfig: '',
                          jdk: 'jdk17',
                          maven: 'maven3',
                          mavenSettingsConfig: '',
                          traceability: true) {
                    sh 'mvn package'
                }
            }
        }
        stage('sonar-scan') {
            steps {
                withSonarQubeEnv(credentialsId: 'sonar-key') {
                    sh 'mvn clean package sonar:sonar'
                }
            } 
        }
    }
}
