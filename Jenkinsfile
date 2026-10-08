pipeline {

    agent any

    parameters {

        choice(
            name: 'ENVIRONMENT',
            choices: ['dev', 'qa', 'uat'],
            description: 'Select target environment'
        )

        booleanParam(
            name: 'RUN_TESTS',
            defaultValue: true,
            description: 'Execute application tests'
        )
    }

    environment {

        APP_NAME = 'quickcart-order-service'

        APP_VERSION = '1.0'
    }

    stages {

        stage('Initialize') {

            steps {

                echo "Job: ${env.JOB_NAME}"

                echo "Build: ${env.BUILD_NUMBER}"

                echo "Workspace: ${env.WORKSPACE}"

                echo "Target: ${params.ENVIRONMENT}"

                echo "Run Tests: ${params.RUN_TESTS}"
            }
        }

        stage('Build') {

            steps {

                echo "Building ${APP_NAME}"

                echo "Version ${APP_VERSION}"
            }
        }

        stage('Test') {

            when {

                expression {
                    return params.RUN_TESTS
                }
            }

            steps {

                timeout(time: 2, unit: 'MINUTES') {

                    echo 'Running QuickCart tests'

                    echo 'Tests completed successfully'
                }
            }
        }

        stage('Package') {

            steps {

                retry(3) {

                    echo 'Creating QuickCart application package'
                }
            }
        }
    }

    post {

        success {

            echo 'QuickCart Pipeline SUCCESS'
        }

        failure {

            echo 'QuickCart Pipeline FAILED'
        }

        always {

            echo "Build ${env.BUILD_NUMBER} completed"
        }
    }
}
