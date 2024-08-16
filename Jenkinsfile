pipeline {
    agent any

    environment {
        // Definir as credenciais do Git como uma variável de ambiente
        GIT_CREDENTIALS_ID = 'duducosmos'
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clonar o repositório Git da branch 'main'
                git branch: 'main', credentialsId: "${GIT_CREDENTIALS_ID}", url: 'https://github.com/duducosmos/devopsaula23.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Construir a imagem Docker para a aplicação Flask
                   sh 'docker build -t flask-app .'
                }
            }
        }

        stage('Run Docker Compose') {
            steps {
                script {
                    sh 'docker ps -q --filter "ancestor=flask-app" | xargs -r docker stop'
                    sh 'docker ps -q --filter "ancestor=flask-app" | xargs -r docker rm'
                    // Executar Docker Compose para levantar os serviços
                    // Executa a aplicação
                    sh 'docker run -d -p 5001:5000 flask-app'
                }
            }
        }

        stage('Test Application') {
            steps {
                script {
                    // Testar a aplicação Flask
                    echo 'Teste'
                   
                }
            }
        }
    }

    post {
        always {
            // Limpeza geral após a execução do pipeline
             echo 'Deploy da aplicação...'
            
        }
        success {
            // Ações específicas em caso de sucesso do pipeline
            echo 'Pipeline executado com sucesso!'
        }
        failure {
            // Ações específicas em caso de falha do pipeline
            echo 'O pipeline falhou.'
        }
    }
}
