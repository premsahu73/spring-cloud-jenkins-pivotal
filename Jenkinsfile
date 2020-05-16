pipeline {

    agent any

    stages {

        stage ('Build') {
            steps {
                withMaven(maven: 'D:\\Configuration\\apache-maven-3.5.2') {
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

                    bat '/usr/local/bin/cf login -a http://api.run.pivotal.io -u $USERNAME -p $PASSWORD'
                    bat '/usr/local/bin/cf push'
                }
            }

        }

    }

}