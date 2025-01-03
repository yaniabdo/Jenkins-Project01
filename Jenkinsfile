pipeline {
    agent {
        label 'slave1'
    }
    
    environment {
        SCRIPT_NAME = ''
        SCRIPT_AGE = ''
    }
    
    stages {
        stage('Process JSON and Execute Script') {
            steps {
                script {
                    // Read JSON content
                    def jsonString = sh(script: 'cat parameters.json', returnStdout: true).trim()
                    
                    // Convert the LazyMap to a regular map to avoid serialization issues
                    def props = new groovy.json.JsonSlurperClassic().parseText(jsonString)
                    def name = props.name.toString()
                    def age = props.age.toString()
                    
                    // Execute with parameters
                    withEnv(["SCRIPT_NAME=${name}", "SCRIPT_AGE=${age}"]) {
                        sh """
                            chmod +x script.sh
                            ./script.sh
                        """
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
