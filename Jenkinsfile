pipeline {

    agent any

    stages {

        stage ('Build') {
            steps {
                withMaven() {
                    bat 'mvn clean package'
                }
            }
        }

        stage ('Deploy') {
            steps {

                withCredentials([[$class          : 'UsernamePasswordMultiBinding',
                                  credentialsId   : 'PCF_LOGIN',
                                  usernameVariable: 'USERNAME',
                                  passwordVariable: 'PASSWORD']]) {
                    bat 'cd D:\\log\\cf-cli-installer_6.43.0_winx64'
                    bat 'cf login -a https://api.run.pivotal.io -u $USERNAME -p $PASSWORD'
                    bat 'cf push'
                }
            }

        }

    }

}