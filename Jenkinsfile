pipeline {
    agent none

    stages {
        stage('Test') {
            agent {
                node { label 'test-node' }
            }
            when {
                branch 'develop'
            }
            steps {
                checkout scm
                // Add commands to run tests on test node
                sh 'echo "Running tests on test node..."'
                // Example: run test commands, e.g., npm install, npm test
            }
        }
        
        stage('Deploy to Prod') {
            agent {
                node { label 'prod-node' }
            }
            when {
                branch 'develop'
                beforeAgent true
            }
            steps {
                // Only trigger this stage if the Test stage was successful
                input 'Deploy to production?'
                sh 'echo "Copying files to production node..."'
                // Example: deploy to production, e.g., scp to prod server
            }
        }
    }

    post {
        success {
            echo 'Deployment pipeline was successful!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
