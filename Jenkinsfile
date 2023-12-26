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

        stage('Build and Package') {
            steps {
                withMaven(globalMavenSettingsConfig: '',
                          jdk: 'jdk17',
                          maven: 'maven3',
                          mavenSettingsConfig: '',
                          traceability: true) {
                    sh 'mvn install'
                }
            }
        }
    }
}
