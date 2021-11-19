pipeline {
    agent any
    environment{
      SERVER_USER = "ubuntu"
      DOMAIN_IP = "18.132.227.51"

    }
    stages {

        //Configuration to deploy to staging
        stage('Build') {
            //setting configuration to deploy the develop branch
            when {
              branch 'develop'
            }  // ssh Publisher to transfer files  from jenkins to staging server
            steps{
                sshPublisher(
                         failOnError: true,
                         continueOnError: false,
                         publishers: [
                            sshPublisherDesc(
                                 configName: 'thrive-staging', //Server configuration setup  in jekins setting
                                  verbose: true,
                                 transfers: [
                                     sshTransfer(
                                          sourceFiles: '**/public_html/', //copy projejct files after checking out from source control
                                          //removePrefix: 'public_html/',
                                          excludes:'**/wp-config.php, **/robots.txt',
                                          remoteDirectory: 'thrivebuild', //create a directory
                                         execCommand: 'sudo rsync -a thrivebuild/public_html/ /var/www/thrive/public_html/   && sudo chown -R ubuntu:ubuntu /var/www/thrive/public_html && sudo chmod -R 755 /var/www/thrive/public_html' //execute command after file transfer
					                  )
                                  ]
                            )
                        ]
                    )


            }
        }
        //End of DeployToStaging Configuration





    }
}
