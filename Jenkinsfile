pipeline {
    agent any

    tools { 
        maven 'maven3' 
        jdk 'jdk17' 
    }
    enviornment{
        SCANNer_HOME= tool 'sonarqube'
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
                script {
                    withMaven(
                        maven: 'maven3',
                        jdk: 'jdk17',
                        mavenSettingsConfig: '',
                        mavenLocalRepo: '.m2repo',
                        options: [findbugsPublisher(), jacocoPublisher()]
                    ) {
                        sh 'mvn clean'
                    }
                }
            }
        }

        stage('Compile') {
            steps {
                script {
                    withMaven(
                        maven: 'maven3',
                        jdk: 'jdk17',
                        mavenSettingsConfig: '',
                        mavenLocalRepo: '.m2repo',
                        options: [findbugsPublisher(), jacocoPublisher()]
                    ) {
                        sh 'mvn compile'
                    }
                }
            }
        }

        stage('Package') {
            steps {
                script {
                    withMaven(
                        maven: 'maven3',
                        jdk: 'jdk17',
                        mavenSettingsConfig: '',
                        mavenLocalRepo: '.m2repo',
                        options: [findbugsPublisher(), jacocoPublisher()]
                    ) {
                        sh 'mvn package'
                    }
                }
            }
        }

        stage('SonarQube Scan') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-key') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            } 
        }
    }
}
