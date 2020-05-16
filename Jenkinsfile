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

                    bat 'D:\\log\\cf-cli-installer_6.43.0_winx64 cf login -a http://api.run.pivotal.io -u $USERNAME -p $PASSWORD'
                    bat 'D:\\log\\cf-cli-installer_6.43.0_winx64 cf push'
                }
            }

        }

    }

}