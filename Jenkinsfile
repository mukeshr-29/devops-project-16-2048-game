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
        stage('sonarqube analysis'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube'){
                        sh '''
                           $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=2048_game \
                           -Dsonar.projectKey=2048_game 
                        '''
                    }
                }
            }
        }
        stage('quality gate check'){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube'
                }
            }
        }
        stage('install npm'){
            steps{
                sh 'npm install'
            }
        }
    }
}