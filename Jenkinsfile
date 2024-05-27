pipeline {
    agent any
    parameters {
        string(name:'Env',defaultValue:'Test',description:'Env to display')
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
            }
        }
        stage('Package') {
            agent {label 'Slave1'}
            steps {
               echo "Package the code in env: ${params.Env}"
            }
        }
         stage('Deploy') {
            steps {
               echo "Deploy the code"
            }
        }
    }
}
