pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script {
                    // Get the list of changes
                    def changes = currentBuild.changeSets.collectMany { it.items }

                    // Check if any commit contains the keyword '[trigger]'
                    def triggerCommit = changes.find { it.msg.contains('[trigger]') }

                    if (triggerCommit) {
                        echo "Pipeline triggered by commit: ${triggerCommit.msg}"
                        docker.build('eatherv/some', './')
                    } else {
                        echo "No relevant commit message found. Skipping build."
                        currentBuild.result = 'NOT_BUILT'
                    }
                }
            }
        }
    }
}
