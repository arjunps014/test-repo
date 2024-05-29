pipeline {
    agent any

    stages {
        stage('BRANCH') {
            when { env.GIT_BRANCH == "origin/main" }
            steps {
                script {
                    echo "BRANCH: ${env.GIT_BRANCH}"
                    sh 'ls -la'
                }
            }
        }
        stage('TAG') {
            when { env.GIT_BRANCH =~ /refs\/tags\/v.*/ }
            steps {
                script {
                    echo "TAG: ${env.GIT_BRANCH}"
                    sh 'ls -la'
                }
            }
        }
    }
}
