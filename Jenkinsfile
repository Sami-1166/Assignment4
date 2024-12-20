pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                // Clone your GitHub repository
                git branch: 'main', url: 'https://github.com/Sami-1166/Assignment4.git'
            }
        }
        stage('Deploy to Apache') {
            steps {
                // Transfer index.html to the Apache server
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'apache-server',  // Matches the SSH config name
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'index.html',
                                    remoteDirectory: '/var/www/html/'
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }
}