def notify() {
       emailext (
       subject: "job started"
              //${status}: Job ${env.JOB_NAME} ([${env.BUILD_NUMBER})",
       body: """
       Check console output at <a href="${env.BUILD_URL}">${env.JOB_NAME} (${env.BUILD_NUMBER})</a>""",
       to: "${BUILD_USER_EMAIL}",
       from: 'shaileshubhe77@gmail.com')
}
pipeline{
    agent any
    stages {
        //notify('Started')
        stage ('Checkout'){ 
            steps {       
                checkout changelog: false, 
                scm: [$class: 'GitSCM', 
                branches: [[name: '*/master']], 
                doGenerateSubmoduleConfigurations: false, 
                extensions: [], 
                submoduleCfg: [], 
                userRemoteConfigs: [[url: 'https://github.com/ganeshhp/helloworldweb.git']]]
            }
        }

        stage ('Creating package'){
            steps {
                sh label: '', script: 'mvn package'
            }
        }
        //notify ('Waiting for Deployment')
        //input 'Deploy to Staging?'
        stage ('Artifacts'){
            steps {
                archiveArtifacts 'target/*.war'
            }
        }


        }
       notify('Completed')  
}
