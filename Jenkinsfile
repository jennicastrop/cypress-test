pepeline{
    agent any
    
    parameters {
        string(name: 'SPEC', defaultValue: "cypress/e2e/1-getting-started/**", description: "Enter the scripts path that you want to execute")
        choice(name: "BROWSER", choices: ['chrome', 'firefox'], description: "Choice the browser to execute the scripts")
    }

    options{
        ansiColor('xterm')
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

    post{
        always{
            publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: true, reportDir: 'cypress/report', reportFiles: 'indes.html', reportName: 'HTML report, reportTitles: ''])
        }
    }
}
