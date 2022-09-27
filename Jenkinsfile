pipeline {
    agent any

    environment {
    BUILD_SCRIPTS_GIT="https://github.com/trungle98/test-jenkins.git"
    BUILD_SCRIPTS='mypipeline'
    BUILD_HOME='/var/lib/jenkins/workspace'
    } 

    post {
        always {
            echo 'One way or another, I have finished'
            deleteDir() /* clean up our workspace */
        }
        success {
            echo 'I succeeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }

    stages { 
        stage('Clone') {
            //implement pipeline code 
            steps {
                
                sh "mkdir -p $WORKSPACE/repo;\
                    git config --global user.email 'trungle98hn@gmail.com';\
                    git config --global user.name 'anthony';\
                    git config --global push.default simple;\
                    git clone $BUILD_SCRIPTS_GIT repo/$BUILD_SCRIPTS"
                sh "chmod -R +x $WORKSPACE/repo/$BUILD_SCRIPTS"
            }
        }
        stage('Build') {
            steps{
                nodejs(nodeJSInstallationName: 'Node 6.x', configId: '<config-file-provider-id>'){
                    sh "cd $WORKSPACE/repo/$BUILD_SCRIPTS;\
                        npm install;\
                        npm run build;\
                        USE_SSH npm run deploy;\
                "
                }

            }

            //implement pipeline code 
        }
    }
}