pipeline{
    agent any

    parameters {
        string(name: 'SPEC', defaultValue: "cypress/e2e/1-getting-started/**", description: "Enter the scripts path that you want to execute")
        choice(name: "BROWSER", choices: ['chrome', 'firefox'], description: "Choice the browser to execute the scripts")
    }
    
    stages{
        stage('Clone') {
            steps {
                withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
                    sh 'git clone https://$GITHUB_TOKEN@github.com/jennicastrop/cypress-test.git'
                }
            }
        }
        stage('Testing'){
            steps{
                sh "npm i"
                sh "npx cypress run --browser ${BROWSER} --spec ${SPEC}"
            }
        }
    }
}
