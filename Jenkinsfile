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
        stage('Build') {
            steps {
                sh 'curl -sL https://deb.nodesource.com/setup_16.x | bash -'
                sh 'apt-get install -y nodejs'
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
