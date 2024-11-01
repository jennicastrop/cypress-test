pipeline{
    agent any

    parameters {
        string(name: 'SPEC', defaultValue: "cypress/e2e/1-getting-started/**", description: "Enter the scripts path that you want to execute")
        choice(name: "BROWSER", choices: ['chrome', 'firefox'], description: "Choice the browser to execute the scripts")
    }
    
    stages{
        stage('Clone') {
            steps {
                script {
                    def repoDir = 'cypress-test'
                    if (fileExists(repoDir)) {
                        echo "Deleting existing repo directory: ${repoDir}"
                        sh "rm -rf ${repoDir}"
                    }
                    
                    withCredentials([string(credentialsId: 'github-token', variable: 'GITHUB_TOKEN')]) {
                        sh "git clone https://${GITHUB_TOKEN}@github.com/jennicastrop/cypress-test.git ${repoDir}"
                    }
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                dir('cypress-test') {
                    sh 'npm install'
                    sh "npm install --no-color"
                }
            }
        }
        stage('Testing'){
            steps{
                dir('cypress-test') {
                    sh "npx cypress run --browser ${BROWSER} --spec ${SPEC}"
                }
            }
        }
    }
    post {
        always {
            publishHTML([
                allowMissing: false,
                alwaysLinkToLastBuild: false,
                keepAll: true,
                reportDir: 'cypress/report',
                reportFiles: 'index.html',  // Corrected the file name
                reportName: 'HTML report',
                reportTitles: ''
            ])
        }
    }
}
