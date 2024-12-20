pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                // Clone the GitHub repository from the 'main' branch
                git branch: 'main', url: 'https://github.com/Sami-1166/Assignment4.git'
            }
        }
        stage('Deploy to Apache') {
            steps {
                // Transfer the index.html file to the Apache server and fix its location
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'apache-server', // Matches the SSH config in Jenkins
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/index.html', // Matches the file pattern
                                    remoteDirectory: '/var/www/html/', // Correct target directory
                                    removePrefix: '', // No prefix to remove
                                    cleanRemote: false // Keep existing files in the directory
                                )
                            ],
                            execCommand: '''
                                echo "Checking file location:"
                                ls -l /var/www/html/var/www/html/
                                echo "Moving the file to /var/www/html"
                                sudo mv /var/www/html/var/www/html/index.html /var/www/html/
                                echo "Verifying the move:"
                                ls -l /var/www/html/
                            ''',
                            execTimeout: 60000 // Timeout for the command execution
                        )
                    ]
                )
            }
        }
    }
}
