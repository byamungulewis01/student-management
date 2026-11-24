// (Activity 13 = Build stage only. See git tag activity-13)
// pipeline {
//     agent any

//     stages {
//         stage('Build') {
//             steps {
//                 echo 'Starting DevOps application build...'
//                 sh 'docker --version'
//                 sh 'docker build -t devops-app:1.0 .'
//                 echo 'Docker image build completed!'
//             }
//         }
//         stage('Deploy') {
//             steps {
//                 sh 'docker rm -f devops-web || true'
//                 sh 'docker run -d --name devops-web -p 8081:80 devops-app:1.0'
//             }
//         }
        
//     }

//     post {
//         success { echo 'SUCCESS: DevOps application built successfully.' }
//         failure { echo 'FAILURE: Check the Jenkins Console Output.' }
//         always  { echo 'Jenkins pipeline execution finished.' }
//     }
// }

// ACTIVITY 14: Automated unit and integration tests in the pipeline

pipeline {
    agent any

    triggers {
        pollSCM('H/2 * * * *')
    }

    stages {

        // Stage 1: Install testing dependencies
        stage('Install Dependencies') {
            steps {
                echo 'Installing testing dependencies...'
                sh 'npm ci'
                echo 'Dependencies installed successfully!'
            }
        }

        // Stage 2: Test HTML files
        stage('Unit Testing') {
            steps {
                echo 'Testing HTML page existence and structure...'
                sh 'npm run test:unit'
                echo 'Unit tests completed successfully!'
            }
        }

        // Stage 3: Test page links
        stage('Integration Testing') {
            steps {
                echo 'Testing navigation between pages...'
                sh 'npm run test:integration'
                echo 'Integration tests completed successfully!'
            }
        }

        // Stage 4: Build Docker image (from Activity 13)
        stage('Build') {
            steps {
                echo 'Starting DevOps application build...'
                sh 'docker --version'
                sh 'docker build -t devops-app:1.0 .'
                echo 'Docker image build completed!'
            }
        }
    }

    post {
        success { echo 'SUCCESS: All tests passed and Docker image built.' }
        failure { echo 'FAILURE: Check the Jenkins Console Output.' }
        always  { echo 'Jenkins pipeline execution finished.' }
    }
}