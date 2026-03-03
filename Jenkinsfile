pipeline {
    agent any
    stages {
        stage('Failing stage'){
            steps {
                sh 'exit 1' // This command will cause the stage to fail
            }
            post {
                failure{
                    echo 'This runs only if the stage fails'
                }
                always {
                    echo 'This runs regardless of the stage result'
                }
            }
        }
    }
    post {
        failure{
            echo 'Failure Notifying from post section of the pipeline'
        }
        success {
            echo 'No Failures in the pipeline - Successfully ran'
        }
    }
}