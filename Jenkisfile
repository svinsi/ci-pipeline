pipeline {
    agent any
    stages {
        stage('Check if merge to main/master') {
            steps {
                script {
                    def isMergeCommit = sh(script: "git log -1 --pretty=%B | grep 'Merge pull request #'", returnStdout: true).trim()
                    if (isMergeCommit == "") {
                        echo "This is not a merge commit to main/master. Skipping further steps."
                        currentBuild.result = 'NOT_BUILT'
                        return
                    }
                    echo "This is a merge commit to main/master. Proceeding with the pipeline."
                }
            }
        }
        stage('Clone Repository') {
            steps {
                checkout scm
            }
        }
    }
}
