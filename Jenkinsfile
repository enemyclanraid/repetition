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
        stage('Info') {
            steps {
                echo "Ветка: ${env.GIT_BRANCH}"
                echo "Коммит: ${env.GIT_COMMIT}"
            }
        }
        stage('Parallel Tests') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo 'Юнит-тесты...'
                        // Здесь могут быть реальные команды тестирования
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo 'Интеграционные тесты...'
                        // Здесь могут быть реальные команды интеграции
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo "Деплой в окружение: ${params.ENV}"
                // Здесь может быть команда деплоя, например:
                // sh './deploy.sh ${params.ENV}'
            }
        }
    }
    post {
        success {
            telegramSend message: "✅ Jenkins: Сборка успешно завершена!", chatId: '7217764287'
        }
        failure {
            telegramSend message: "❌ Jenkins: Сборка завершилась ошибкой!", chatId: '7217764287'
        }
    }
}

