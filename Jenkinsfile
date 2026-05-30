```groovy
pipeline {

    agent any

    environment {
        REPO_URL = 'https://github.com/medasarisaikumar99-cmd/DEMOS.git'
        BRANCH = 'master'
        CREDS = 'github'
    }

    stages {

        stage('Checkout Code') {
            steps {

                git branch: "${BRANCH}",
                    url: "${REPO_URL}",
                    credentialsId: "${CREDS}"
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('List Artifacts') {
            steps {
                sh 'ls -l target/'
            }
        }

        stage('Upload To Nexus') {
            steps {

                nexusArtifactUploader(

                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '54.173.208.213:8081',

                    groupId: 'clone-project',
                    version: '1.0-SNAPSHOT',
                    repository: 'project_object',

                    credentialsId: 'nexus',

                    artifacts: [[
                        artifactId: 'clone.project',
                        file: 'target/clone.project-1.0-SNAPSHOT.jar',
                        type: 'jar'
                    ]]
                )
            }
        }
    }

    post {

        success {
            echo 'BUILD SUCCESS'
        }

        failure {
            echo 'BUILD FAILURE'
        }
    }
}
```

