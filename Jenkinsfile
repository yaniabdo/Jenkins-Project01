pipeline {
    agent {
        label 'slave1'    // Make sure this matches your slave node label

    }
    
    parameters {
        string(name: 'NAME', defaultValue: '', description: 'Your name')
        string(name: 'AGE', defaultValue: '', description: 'Your age')
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Read Parameters') {
            steps {
                script {
                    // Read JSON file and parse it properly
                    def jsonContent = readFile(file: 'parameters.json')
                    def props = readJSON(text: jsonContent)
                    env.name = props.name
                    env.age = props.age
                }
            }
        }
        
        stage('Execute Script') {
            steps {
                sh 'chmod +x script.sh'
                sh './script.sh'
            }
        }
    }
}
