pipeline {
    agent any
    //parameters {
        //string(name:'Env',defaultValue:'Test',description:'Env to display')
        //booleanParam(name:'ExecuteTests',defaultValue:True,description:'decide to run tc')
        //choice(name:APPVERSION,choices['1.1','1.2','1.3'])
    //}
    //tools {
        // Install the Maven version configured as "M3" and add it to the path.
        //maven "mymaven"
    //}
        environment{
        BUILD_SERVER='ec2-user@172.31.20.56'
    }

    stages {
        stage('Compile') {
            steps {
               echo "compiling the code"
                sh 'mvn compile'
            }
        }
        stage('UnitTest') {
            steps {
               echo "Test the code"
                sh 'mvn test'
            }
            post{
                always{
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Package') {
            agent any
            steps {
                sshagent(['build-server-key']) {
                   echo 'Package using Slave 2 via SSH Agent Plugin'
                    sh "scp -o StrictHostKeyChecking=no server-config.sh ${BUILD_SERVER}:/home/ec2-user"
                    sh "ssh -o StrictHostKeyChecking=no ${BUILD_SERVER} bash ~ec2-user/server-config.sh"
               }
               //echo "Package the code in env: ${params.Env}"
            }
        }
         //stage('Deploy') {
             //input{
                 //message "Provide Approval for Prod"
                 //ok "Deploy to Prod"
                 //parameters{
                    // booleanParam(name:'DeploytoPROD',defaultValue:False,description:'decide to run in Prod')
                 //}
             //}
            //steps {
               //echo "Deploy the code"
            //}
        //}
    }
}
