pipeline{
    agent any
    tools{
      jdk 'jdk17'
      nodejs 'node16'  
    }
    environment{
        SCANNER_HOME=tool 'sonar_scanner'
    }
    stages{
        stage('clean work space'){
            steps{
                cleanWs()
            }
        }
        stage('git checkout'){
            steps{
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/mukeshr-29/devops-project-16-2048-game.git'
            }
        }
    }
}