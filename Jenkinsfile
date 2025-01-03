pipeline {
    agent {
        label 'slave1'
    }
    
    environment {
        SCRIPT_NAME = ''
        SCRIPT_AGE = ''
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
                    
                    // Set environment variables using withEnv
                    withEnv(["SCRIPT_NAME=${props.name}", "SCRIPT_AGE=${props.age}"]) {
                        sh """
                            echo "Name from env: \$SCRIPT_NAME"
                            echo "Age from env: \$SCRIPT_AGE"
                            
                            # Update the script to use these environment variables
                            echo '#!/bin/bash' > script.sh
                            echo 'echo "Hello, I am \$SCRIPT_NAME and I am \$SCRIPT_AGE years old"' >> script.sh
                            chmod +x script.sh
                            ./script.sh
                        """
                    }
                }
            }
        }
    }
}
