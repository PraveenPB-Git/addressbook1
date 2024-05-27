pipeline {
    agent any
    parameters {
        string(name:'Env',defaultValue:'Test',description:'Env to display')
        //booleanParam(name:'ExecuteTests',defaultValue:True,description:'decide to run tc')
        //choice(name:APPVERSION,choices['1.1','1.2','1.3'])
    }
    //tools {
        // Install the Maven version configured as "M3" and add it to the path.
        //maven "mymaven"
    //}

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
            agent {label 'Slave1'}
            steps {
               echo "Package the code in env: ${params.Env}"
                sh 'mvn package'
            }
        }
         stage('Deploy') {
             input{
                 message "Provide Approval for Prod"
                 ok "Deploy to Prod"
                 parameters{
                     booleanParam(name:'DeploytoPROD',defaultValue:False,description:'decide to run in Prod')
                 }
             }
            steps {
               echo "Deploy the code"
            }
        }
    }
}
