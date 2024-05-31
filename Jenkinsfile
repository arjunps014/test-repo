pipeline {
    agent any

    stages {
        stage('BRANCH') {
            when {
                expression { env.GIT_BRANCH == "origin/main" }
            }
            steps {
                script {
                    echo "BRANCH: ${env.GIT_BRANCH}"
                    sh 'ls -la'
                }
            }
        }
        stage('TAG') {
            when {
                expression { env.GIT_BRANCH =~ /refs\/tags\/v.*/ }
            }
            steps {
                script {
                    if (env.GIT_BRANCH.startsWith('refs/tags/')) {
                        env.TAG_NAME = env.GIT_BRANCH.replaceFirst('refs/tags/', '')
                        echo "Tag Name: ${env.TAG_NAME}"
                    }
                    echo "TAG: ${env.GIT_BRANCH}"
                    sh 'ls -la'
                }
            }
        }
    }
}
