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
        stage ('execute unit test')
        {
            steps { withMaven(globalMavenSettingsConfig: '', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                { sh 'mvn test' }
            }
                
            }
        }
    }
}
