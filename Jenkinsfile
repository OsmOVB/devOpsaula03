pipeline {
    agent any
    environment {
        REPO_URL = 'https://github.com/OsmOVB/devOpsaula03.git' // URL do repositório GitHub
        SSH_KEY_CREDENTIAL_ID = 'my-ssh-key-id' // ID das credenciais SSH
    }
    stages {
        stage('Preparação') {
            steps {
                // Configurar chave SSH para acessar o repositório
                sshagent(credentials: [SSH_KEY_CREDENTIAL_ID]) {
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
