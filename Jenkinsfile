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
        stage('Build') {
            steps {
                echo 'Сборка проекта...'
                // Здесь ваши команды сборки
            }
        }
        stage('Test') {
            steps {
                echo 'Запуск тестов...'
                // Здесь ваши команды тестирования
            }
        }
        stage('Deploy') {
            steps {
                echo "Деплой в окружение: ${params.ENV}"
                // Здесь команда деплоя
            }
        }
    }
    post {
        success {
            script {
                def botToken = '7726714649:AAHor72lZ5zv3dlz60tT09gIDgLcAAJ9l6I'
                def chatId = '7217764287'
                def message = "✅ Jenkins: Сборка успешно завершена!\nJob: ${env.JOB_NAME}\nBuild: #${env.BUILD_NUMBER}"
                sh """
                    curl -s -X POST "https://api.telegram.org/bot${botToken}/sendMessage" \
                    -d chat_id=${chatId} \
                    --data-urlencode text="${message}"
                """
            }
        }
        failure {
            script {
                def botToken = '7726714649:AAHor72lZ5zv3dlz60tT09gIDgLcAAJ9l6I'
                def chatId = '7217764287'
                def message = "❌ Jenkins: Сборка завершилась ошибкой!\nJob: ${env.JOB_NAME}\nBuild: #${env.BUILD_NUMBER}"
                sh """
                    curl -s -X POST "https://api.telegram.org/bot${botToken}/sendMessage" \
                    -d chat_id=${chatId} \
                    --data-urlencode text="${message}"
                """
            }
        }
    }
}
