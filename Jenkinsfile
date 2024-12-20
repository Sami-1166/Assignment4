pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository to the Jenkins workspace
                git branch: 'main', url: 'https://github.com/Sami-1166/Assignment4.git'
            }
        }
        stage('Deploy to Apache') {
            steps {
                // Transfer index.html to the Apache server's web directory
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'apache-server',  // Must match SSH config in Jenkins
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'index.html',  // Update if in a subdirectory
                                    remoteDirectory: '/var/www/html/',  // Apache's web directory
                                    removePrefix: '',  // Adjust if sourceFiles is in a subdirectory
                                    cleanRemote: false // Set to true if you want to remove existing files
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }
}
