pipeline {
    agent any
    parameters {
        choice(
            name: 'ENV',
            choices: ['dev', 'prod'],
            description: 'Окружение'
        )
    }
    stages {
        stage('Parallel Tests') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo 'Юнит-тесты...'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo 'Интеграционные тесты...'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Деплой в окружение: ${params.ENV}"
            }
        }
    }
}

