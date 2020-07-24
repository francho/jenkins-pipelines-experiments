pipeline {
    agent any

    parameters {
        choice(choices: 'dev\nprod\n', description: 'Select env to build', name: 'MY_ENVIRONMENT')
    }

    stages {
        stage('Initial Notification') {
            steps {                 //put webhook for your notification channel
                echo 'Pipeline Start Notification'
            }
        }

        stage('Print Env') {
            teps {
                sh 'printenv'
            }
        }

        stage('Vars Testing') {
            environment {
                MY_STAGE_VAR = 'hi dude'
            }

            steps {
                echo 'Robot Testing Start'
                echo "MY_ENVIRONMENT = ${ MY_ENVIRONMENT }"
                echo "MY_STAGE_VAR = ${ env.MY_STAGE_VAR }"
                withCredentials([string(credentialsId: 'SECRET_TEXT', variable: 'SECRET_TEXT_VAR')]) {
                    echo "SECRET_TEXT_VAR = ${ SECRET_TEXT_VAR }"
                }
            }
            post {
                success {
                    echo 'Robot Testing Successfully'
                }
                failure {
                    echo 'Robot Testing Failed'
                }
            }
        }
    }
}
