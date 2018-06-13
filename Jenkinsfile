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

  stage('Start instance') {

          //sh 'docker-machine rm -f  node1-nginx'     
          sh 'docker-machine stop node1-nginx || docker-machine start node1-nginx && docker-machine regenerate-certs -f node1-nginx || docker-machine create --driver amazonec2 --amazonec2-instance-type t2.micro --amazonec2-region eu-west-1 --amazonec2-open-port 80 --amazonec2-open-port 443 --amazonec2-vpc-id vpc-6440e402 node1-nginx'
          //sh 'docker-machine start node1-nginx'
          sh 'docker-machine ip node1-nginx'  
      
      
      
          sh 'eval $(docker-machine env node1-nginx)'
     // sh 'docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q) && docker rmi $(docker images -q)'
          //sh 'docker-machine use node1-nginx'
          sh 'docker run -d -p 80:80 -p 443:443 slodov/sen || docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q) && docker rmi -f $(docker images -q) && docker run -d -p 80:80 -p 443:443 slodov/sen'
                  
   }   
 
   
    
}
