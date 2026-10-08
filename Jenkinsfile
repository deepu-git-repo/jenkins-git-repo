pipeline {

    agent any
environment {

    APP_NAME = 'quickcart-order-service'

    APP_VERSION = '1.0'
}
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
    stages {

        stage('Initialize') {

    steps {

        echo "Job Name: ${env.JOB_NAME}"

        echo "Build Number: ${env.BUILD_NUMBER}"

        echo "Workspace: ${env.WORKSPACE}"
        echo "Target Environment: ${params.ENVIRONMENT}"

        echo "Run Tests: ${params.RUN_TESTS}"
    }
           
}

        stage('Build') {

    steps {

        echo "Application: ${APP_NAME}"

        echo "Version: ${APP_VERSION}"

        echo "Jenkins Build Number: ${env.BUILD_NUMBER}"
    }
}
        stage('Test') {

    when {

        expression {
            return params.RUN_TESTS
        }
    }

    steps {

        timeout(time: 5, unit: 'SECONDS') {

    echo 'Running QuickCart tests'

    bat 'powershell -Command "Start-Sleep -Seconds 10"'

        }
    }
}

    steps {

        echo 'Running QuickCart tests'

        echo 'Tests completed successfully'
    }
}

        stage('Package') {
            steps {
                echo 'Creating QuickCart package'
            }
        }
    }
}
