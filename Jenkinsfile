pipeline {
    agent any

    stages {
        stage('Gavs Build to Stage') {
            steps {
              withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '7675881', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                sshPublisher(
                    failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: 'staging',
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'src/**',
                                    removePrefix: 'src/'
                                )
                            ]
                        )
                    ]
                )
                echo 'Gavs project is now building to STAGE'
                sh 'ls'
              }

           }
        }
        stage('Gavs Build to Production') {
            steps {
              input 'Does the staging environment look OK?'
              milestone(1)
              withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: '7675881', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
                sshPublisher(
                    failOnError: true,
                    publishers: [
                        sshPublisherDesc(
                            configName: 'production',
                            transfers: [
                                sshTransfer(
                                    sourceFiles: 'src/**',
                                    removePrefix: 'src/'
                                )
                            ]
                        )
                    ]
                )
                echo 'Gavs project is now building to Production'
                sh 'ls'
              }

           }
        }

    }
}
