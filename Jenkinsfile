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
                    // Print the contents of parameters.json
                    sh 'cat parameters.json'
                    
                    def jsonString = sh(script: 'cat parameters.json', returnStdout: true).trim()
                    println "JSON String: ${jsonString}"
                    
                    def props = new groovy.json.JsonSlurper().parseText(jsonString)
                    println "Parsed properties: ${props}"
                    
                    env.name = props.name
                    env.age = props.age
                    
                    // Print the environment variables
                    sh 'echo "Name: $name"'
                    sh 'echo "Age: $age"'
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
