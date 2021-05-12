pipeline {
    agent any
    stages {
        stage('Build - Fase 1') {
            steps {
                sh 'echo "Hello World"'
                sh '''
                    echo "Multiline shell steps works too"
                    ls -lah
                '''
            }
        }
        stage('Deploy - Fase 2') {
            steps {
                retry(3) {
                    sh '/tmp/exemplo-deploy.sh'
                    sh 'date'
                }

                timeout(time: 3, unit: 'MINUTES') {
                    retry(5) {
                    sh '/tmp/testa-arquivo.sh'
                    }
                }
            }
        }
        stage('Testes - Fase 3') {
            steps {
                sh 'echo "Fail!"'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
