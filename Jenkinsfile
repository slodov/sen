pipeline {

    agent none

        stages {

            stage('CheckOut') {
                agent { label 'master' }
                    steps {
                         //checkout scm
                        //* ([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/dotronglong/titan-event.git']]])
                    }
            }    

         }
}
