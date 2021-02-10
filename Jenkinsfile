pipeline {
    agent any
    stages {
        stage('Jenkins: Unit Tests') {
            steps {
                sh 'mvn verify -DskipITs=true'
            }
        }
        stage('Jenkins: Integration Tests') {
            steps {
                sh 'mvn verify -DskipUTs=true'
            }
        }
    }
    post {
        always
//         echo 'Cucumber reports...'
//         cucumber failedFeaturesNumber: -1, failedScenariosNumber: -1, failedStepsNumber: -1, fileIncludePattern: '**/*.json', pendingStepsNumber: -1, skippedStepsNumber: -1, sortingMethod: 'ALPHABETICAL', undefinedStepsNumber: -1
        }
        success {
            echo 'Successful test email notification email sent.'
            emailext body: 'This is an email notification from Kevin's test project', subject: 'Email notification from Kevin\'s test project', to: 'kpdwinter@hotmail.com'
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