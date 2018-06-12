node {

    def app

    
            stage('CheckOut') {
                
                  
                         checkout scm
                        //* ([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/dotronglong/titan-event.git']]])
                    
            } 

            stage('Build') {

                    app=docker.build("slodov/sen")

            }   

            stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }

  stage('Start instaance') {

               sh 'docker-machine rm -f  node1-nginx'   
      
      sh 'docker-machine create --driver amazonec2 --amazonec2-instance-type t2.micro --amazonec2-region eu-west-1 --amazonec2-open-port 80 --amazonec2-open-port 443 --amazonec2-vpc-id vpc-6440e402 node1-nginx'

            
            
            }   
   

}
