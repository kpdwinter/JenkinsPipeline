pipeline {
    agent any
    stages {
        stage('Jenkins: Checkout..') {
            sh 'echo "Jenkins Stage: Checkout.. ..."'
            steps {
                sh 'echo "Jenkins Step: Checkout.. ..."'
            }
        }
        stage('Maven compiles and tests') {
            echo 'Jenkins stage: Unit tests...'
            steps {
                echo 'Jenkins Step: Unit tests...'
                sh 'mvn verify - DskipITs = true'
            }
            steps {
                echo 'Jenkins Step: Integration tests...'
                sh 'mvn verify - DskipUTs = true'
            }
            stage('Deploy') {
                echo 'Jenkins stage: Deploy...'
                steps {
                    sh 'echo "Jenkins Step: Project ready for deployment ..."'
                }
            }
        }
        post {
            always {
                echo 'Cucumber reports...'
                cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
            }
            success {
                echo 'I succeeded!'
            }
            unstable {
                echo 'I am unstable :/'
            }
            failure {
                echo 'I failed :('
            }
            changed {
                echo 'Things were different before...'
            }
        }
    }
}