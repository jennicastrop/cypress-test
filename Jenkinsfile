pepeline{
    agent any
    
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
