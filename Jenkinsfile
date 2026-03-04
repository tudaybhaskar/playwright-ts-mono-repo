pipeline {
    agent any
    stages {
        stage('Failing stage'){
            steps {
                echo 'Running stage called : Failing stage'
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE', message: 'Has some Error'){
                    sh 'exit 1' // This command will cause the stage to fail
                }
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
        stage('Usage of script block - Groovy learning'){
            steps{
                script{
                    def browsers = ['chromium', 'firefox', 'webkit']

                    for( browser in browsers ){
                        echo "--- Starting tests for ${browser}"

                        catchError(buildResult: 'SUCCESS', stageResult: 'SUCCESS'){
                            sh 'exit 0'
                        }
                    }
                }
            }
            
        }
        stage('Usage of try-catch - Script - Groovy Learning'){
            steps{
                script{
                    try {
                        sh 'exit 1'
                    } catch (Exception e) {
                        echo "Tests failed, marking build as SUCCESS even there is a failure"
                        currentBuild.result = 'SUCCESS' 
                        // This won't stop the pipeline, it just sets the 'Yellow' flag
                    }
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