node ('ubuntu-app-agent'){
   /*
    environment {
           SNYK_TOKEN = credentials('SYNK')
    } 
   */
    
    def app
 
    stage('Cloning Git') {
        /* Let's make sure we have the repository cloned to our workspace */
       checkout scm
    }
      /*
     stage('SAST') {
       // node('ubuntu'){
         
       ///   sh 'rm -f package-lock.json'
      ///   build 'SNYK-SAST' 
           withCredentials([string(credentialsId: 'sk', variable: 'TOKEN')]) {
          build 'SNYK-SAST'  
            
               println(env.TOKEN)
            snykSecurity(snykInstallation: 'synk-scan', tokenCredentialId : env.TOKEN, additionalArguments: 'test', monitor: true, severity: 'high') 
          
          }
         
               sh 'echo "SAST Test passed "' }
         */


    stage('Build-and-Tag') {
    // sh 'echo "Build-and-Tag"'
       
        /* This builds the actual image; synonymous to
         * docker build on the command line */

       app = docker.build("madsaint/docker:red")
    }

  /*  
   stage('IMAGE-VULNERABILITY-TEST') {
      //  node('master'){
        
       ///     build 'AQUASEC-SECURITY' 
      //  }

           sh 'echo "Image Vulnerability Test passed"'
        
    }
    */

    stage('Post-to-dockerhub') {
     // sh 'echo "Post-to-dockerhub"' 
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
     docker.withRegistry('https://registry.hub.docker.com', 'dochub')
        {
        app.push("latest")
        }
        }
     
     

    stage('Pull-image-server') {
    //  sh 'echo "Pull-image-server"' 
        sh "docker-compose down"
        sh "docker-compose up -d"			
      }
   /*
     stage('DAST') {
        Ideally, we would run a test framework against our image.
         For this example, we're using a Volkswagen-type approach ;-)
        node('ubuntu'){
           // build 'OWASP-ZAP' 

            sh 'echo "DAST Test passed"'
        }
        
    }
    */
   
   
}
