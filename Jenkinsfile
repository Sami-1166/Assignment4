pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository
                git branch: 'main', url: 'https://github.com/Sami-1166/Assignment4.git'
            }
        }
        stage('Deploy to Apache') {
            steps {
                // Transfer index.html directly to /var/www/html
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'apache-server', // Matches the SSH config name
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/index.html', // Match the file pattern
                                    remoteDirectory: '/var/www/html/', // Target the correct directory
                                    removePrefix: '', // No prefix to remove
                                    cleanRemote: false // Keep existing files in the remote directory
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }
}
