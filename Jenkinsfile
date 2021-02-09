pipeline {

    agent any

    options {
        skipStagesAfterUnstable()
    }

    stages {
        stage('Build') {
            steps {
                sh 'echo "Jenkins: Build running ..."'
                sh 'mvn clean compile'
            }

        }
        stage('Run Tests') {
            parallel {
                stage('Surefire Unit Tests...') {
                    agent any
                    steps {
                        sh 'mvn clean test'
                    }
                    post {
                        always {
                            junit "**/TEST-*.xml"
                        }
                    }
                }
                stage('Failsafe integration tests...') {
                    agent any
                    steps {
                        sh 'mvn clean verify -DskipUTs=true'
                    }
                    post {
                        always {
                            junit "**/TEST-*.xml"
                        }
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'echo "Jenkins: Project ready for deployment ..."'
            }
        }
    }
}


