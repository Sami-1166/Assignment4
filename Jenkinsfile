pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Sami-1166/Assignment4.git'
            }
        }
        stage('Deploy to Apache') {
            steps {
                // Transfer the file
                sshPublisher(
                    publishers: [
                        sshPublisherDesc(
                            configName: 'apache-server',
                            transfers: [
                                sshTransfer(
                                    sourceFiles: '**/index.html',
                                    remoteDirectory: '/var/www/html/',
                                    removePrefix: '',
                                    cleanRemote: false
                                )
                            ]
                        )
                    ]
                )
                
                // Move the file after transferring
                sshCommand remote: 'apache-server', command: '''
                    echo "Debugging: Checking file locations before move"
                    ls -l /var/www/html/
                    sudo mv /var/www/html/var/www/html/index.html /var/www/html/
                    echo "Debugging: Checking file locations after move"
                    ls -l /var/www/html/
                '''
            }
        }
    }
}
