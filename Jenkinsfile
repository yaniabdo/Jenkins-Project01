pipeline {
    agent any
    
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
                    def props = readJSON file: 'parameters.json'
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
