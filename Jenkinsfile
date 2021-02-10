pipeline {
    agent any
    stages {
        stage('Jenkins: Checkout..') {
            steps {
                echo "Jenkins: Checkout.. ..."
            }
        }
        stage('Maven compiles and tests') {
            steps {
                echo 'Jenkins Step: Unit tests...'
                sh 'mvn verify -DskipITs=true'

                echo 'Jenkins Step: Integration tests...'
                sh 'mvn verify -DskipUTs=true'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Jenkins stage: Deploy...'
                echo "Jenkins Step: Project ready for deployment ..."
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