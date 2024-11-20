pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    if (currentBuild.changeSets.any { change ->
                        change.msg.contains("[name]")
                    }) {
                        docker.build('eatherv', './')
                    } else {
                        echo "No trigger keyword found."
                        currentBuild.result = 'NOT_BUILT'
                    }
                }
            }
        }
    }
}
