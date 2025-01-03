pipeline {
    agent {
        label 'slave1'
    }
    
    stages {
        stage('Introduction') {
            steps {
                echo 'Script is created by yani'
            }
        }
        
        stage('Execute Script') {
            steps {
                script {
                    // Read and parse JSON directly into environment variables
                    def json = sh(script: 'cat parameters.json', returnStdout: true).trim()
                    def props = readJSON text: json
                    
                    // Set environment variables
                    env.SCRIPT_NAME = props.name
                    env.SCRIPT_AGE = props.age
                    
                    // Execute script
                    sh '''
                        chmod +x script.sh
                        ./script.sh
                    '''
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
