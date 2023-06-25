pipeline {
    
    agent any
    
    tools {
        nodejs 'Node-Latest'
    }
    
    environment {
        VERCEL_TOKEN = credentials('vercel-token')
    }
    
    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/eliud-kinyanjui/vue-lesson-1'
            }
        }
        
        stage('Check Vercel') {
            steps {
                script {
                    def npmModule = 'vercel'
                    def npmCheckCmd = "npm list --depth=0 ${npmModule}"
                    def npmCheckResult = sh(script: npmCheckCmd, returnStatus: true)
                    if (npmCheckResult == 0) {
                        echo "The ${npmModule} module is installed"
                        sh 'vercel --version'
                    } else {
                        echo "The ${npmModule} module is not installed"
                        sh 'npm install -g vercel'
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                //withCredentials([string(credentialsId: 'vercel-token', variable: 'VERCEL_TOKEN')]) {
                   sh "vercel --name vue-app deploy --prod --yes --token ${VERCEL_TOKEN}"
                //}
            }
        }
    }
}