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
                // Transfer index.html directly to the /var/www/html directory
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'apache-server',  // Matches the SSH config name
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'index.html',  // Make sure this matches the file in your repository
                                    remoteDirectory: '/var/www/html/',  // Directly target the Apache root
                                    removePrefix: '',  // Do not add any directory prefix
                                    cleanRemote: false // Do not clean the directory to avoid removing existing files
                                )
                            ]
                        )
                    ]
                )
            }
        }
    }
}
