pipeline {
    agent any

    enviornment {
        GIT_REPO_URL = "https://github.com/arjunps014/test-repo.git"
        GIT_CHECKOUT_TAG = "refs/tags/v5.0.0"
    }

    stages {
        stage ('Git Checkout tags'){
            steps {
                sh 'date'
                checkout([
                    $class: 'GitSCM', 
                    branches: [
                        [
                            name: "${GIT_CHECKOUT_TAG}"
                        ]
                    ], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [
                        [
                            $class: 'CloneOption',
                            reference: '',
                            shallow: true
                        ]
                    ], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [
                        [
                            credentialsId: "${env.GIT_CREDENTIAL_ID}", 
                            url: "${env.GIT_REPO_URL}"
                        ]
                    ]
                ])
            }
        }
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
                expression { env.GIT_BRANCH.startsWith('refs/tags/') }
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
