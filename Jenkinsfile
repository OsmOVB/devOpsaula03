pipeline {
    agent any
    environment {
        REPO_URL = 'git@github.com:OsmOVB/Devops_2024_2.git' // Substitua pela URL do seu repositório GitHub
        SSH_KEY_PATH = "${HOME}/.ssh/id_ed25519"
    }
    stages {
        stage('Preparação') {
            steps {
                // Configurar chave SSH para acessar o repositório
                sshagent(credentials: ['seu-ssh-credential-id']) {
                    sh 'chmod +x ${WORKSPACE}/deploy.sh'
                }
            }
        }
        stage('Clone do Repositório') {
            steps {
                git branch: 'main', url: "${REPO_URL}"
            }
        }
        stage('Executar Script de Deploy') {
            steps {
                sh 'bash ${WORKSPACE}/deploy.sh'
            }
        }
    }
    post {
        success {
            echo 'Pipeline concluída com sucesso!'
        }
        failure {
            echo 'Falha na pipeline. Verifique os logs.'
        }
    }
}
