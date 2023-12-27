pipeline {
    agent any

    tools { 
        maven 'maven3' 
        jdk 'jdk17' 
    }
    environment{
        SCANNER_HOME= tool 'sonarqube'
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
                        sh 'mvn clean compile'
                    }
                }
            }
        }

        stage('DP-check') {
            steps {
                    //dependencyCheck additionalArguments: '--format HTML', odcInstallation: 'DP-check'
                    dependencyCheck additionalArguments: '--project Jenkins_cicd --scan / --format XML ', odcInstallation: 'DP-check'
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
                        sh 'mvn clean package'
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
