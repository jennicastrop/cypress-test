pepeline{
    agent any

    withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
        sh 'git clone https://$GITHUB_TOKEN@github.com/jennicastrop/cypress-test.git'
    }
    
    stages{
        stage('Build'){
            echo "Building the app..."
        }
        stage('Testing'){
            sh "npm i"
            sh "npx cypress run --browser ${BROWSER} --spec ${SPEC}"
        }
        stage('Deploy'){
            echo "Deploying the app..."
        }
    }
}
