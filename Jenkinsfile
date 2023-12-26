pipeline {
    agent any

    tools { 
        maven 'maven3' 
        jdk 'jdk17' 
    }

    stages {
        stage('git checkout') {
            steps {
                git branch: 'main', changelog: false, credentialsId: 'git-login', poll: false, url: 'https://github.com/sandipmooreco/Petclinic.git'
            }
        }
    }
}
