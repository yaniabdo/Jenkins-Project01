pipeline {
    agent {
        label 'slave'
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
                    def jsonString = sh(script: 'cat parameters.json', returnStdout: true).trim()
                    def props = new groovy.json.JsonSlurper().parseText(jsonString)
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
