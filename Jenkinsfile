node {

    def app

    
            stage('CheckOut') {
                
                         checkout scm
            } 

            stage('Build') {

                    app=docker.build("slodov/sen")

            }   

            stage('Push image') {
                
                docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
                app.push("${env.BUILD_NUMBER}")
                app.push("latest")
                }
            }

            stage('Start instance') {
            
                sh 'docker-machine rm -f  node1-nginx'  
                sh 'docker-machine create --driver amazonec2 --amazonec2-instance-type t2.micro --amazonec2-region eu-west-1 --amazonec2-open-port 80 --amazonec2-open-port 443 --amazonec2-vpc-id vpc-6440e402 node1-nginx'
                 ///     sh 'docker-machine stop node1-nginx || (docker-machine start node1-nginx && docker-machine regenerate-certs -f node1-nginx ) || ( docker-machine rm -f  node1-nginx && docker-machine create --driver amazonec2 --amazonec2-instance-type t2.micro --amazonec2-region eu-west-1 --amazonec2-open-port 80 --amazonec2-open-port 443 --amazonec2-vpc-id vpc-6440e402 node1-nginx)'
                 //sh 'docker-machine start node1-nginx'
                sh 'docker-machine ip node1-nginx'  
                sh 'docker info'
                sh 'docker network ls -q'
      
            }   
      
            stage('Start Docker') {
                sh 'export'
                sh 'docker-machine inspect node1-nginx'
                sh 'docker-machine ls'
                sh 'docker ps -a'
                sh 'docker-machine env node1-nginx'
                sh 'eval "$(docker-machine env node1-nginx)"; docker pull slodov/sen && docker run -d -n nginx -p 80:80 -p 443:443 slodov/sen'
           //     sh 'docker-machine ls'  (docker ps | grep nginx && docker stop nginx)
            //    sh 'export'
            //    sh 'docker network ls -q'
                  //   sh 'docker info'
                  //  sh ''
                  // sh 'docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q) && docker rmi $(docker images -q)'
                  //sh 'docker-machine use node1-nginx'
                  ///   sh 'docker run -d -p 80:80 -p 443:443 slodov/sen || (docker stop $(docker ps -a -q) && docker rm $(docker ps -a -q) && docker rmi -f $(docker images -q) && docker run -d -p 80:80 -p 443:443 slodov/sen)'
            //    sh 'docker ps -a' 
           //     sh 'docker run -d -p 80:80 -p 443:443 slodov/sen'
        
           //     sh 'eval $(docker-machine env -u)'        
            }   
 
       
}
