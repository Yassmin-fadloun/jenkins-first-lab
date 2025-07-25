pipeline {
    agent any

    parameters {
        string(name: 'DEPLOY_ENV', defaultValue: 'dev', description: 'Deployment environment (dev/staging/prod)')
    }

    environment {
        APP_NAME = "MyDemoApp"
        BUILD_DIR = "build"
    }

    stages {
        stage('Preparation') {
            steps {
                echo "Cleaning previous builds..."
                sh 'rm -rf $BUILD_DIR || true'
                sh 'mkdir -p $BUILD_DIR'
            }
        }

        stage('Build') {
            steps {
                echo "Building $APP_NAME..."
                sh 'echo "Compiling source code..." > $BUILD_DIR/build.log'
            }
        }

        stage('Test') {
            steps {
                echo "Running unit tests..."
                sh 'echo "Tests passed." >> $BUILD_DIR/build.log'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to ${params.DEPLOY_ENV}..."
                sh 'echo "Deployment successful." >> $BUILD_DIR/build.log'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'build/**', fingerprint: true
            echo "Build artifacts archived."
        }
        always {
            echo "Pipeline completed."
        }
    }
}

