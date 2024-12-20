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
                            configName: 'apache-server',  // Matches the SSH config name
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'index.html',  // Adjust this if it's located in a subdirectory
                                    remoteDirectory: '/var/www/html',  // Apache's web directory
                                    removePrefix: '',  // Optional: Removes the prefix if sourceFiles is in a subdir
                                    cleanRemote: false // Optional: Set to true if you want to remove existing files on the remote
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }
}
