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
        // Other stages can be added here if needed
    }
}
