pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/vastevenson/pytest-intro-vs.git']]])
            }
        }
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/vastevenson/pytest-intro-vs.git'
                sh 'python3 ops.py'
            }
        }
        stage( 'Unit Testing' ) {
            steps {
                script {
                    try {
                        //Move to the correct directory
                        sh 'cd /$WORKSPACE/'
                        //Make sure all of the necessary libraries and plug-ins are installed
                        sh 'sudo apt install python3-pip'
                        sh 'sudo python3 -m pip install pytest'
                        //Execute test in verbose format
                        sh 'pytest tests.py -v'
                    }
                    catch (exc) {
                            echo 'Unit tests failed'
