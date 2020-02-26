def notify(status){
       //emailext body: 'build started', 
    emailext (
       body: """<p> Jenkins Pipeline Notification </p>
            <table border="1" cellpadding="0" cellspacing="0" style="">
                <thead>
                    <tr style=" background:#000; color:#ffffff;text-align:center ">
                        <th colspan="2" style="padding: 4px;"> PipeLine Job Notification </th>
                    
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td style="padding: 4px;">Job Name</td>
                        <td style="padding: 4px;">${env.JOB_NAME}</td>
                    </tr>
            <tr>
                        <td style="padding: 4px;">Job Status</td>
                        <td style="padding: 4px;">${status}</td>
                    </tr>
            <tr>
                        <td style="padding: 4px;">Build Number</td>
                        <td style="padding: 4px;">${env.BUILD_NUMBER}</td>
                    </tr>
            <tr>
                        <td style="padding: 4px;">Build URL</td>
                        <td style="padding: 4px;"><a href="${env.BUILD_URL}"> ${env.BUILD_URL} </a> </td>
                    </tr>
            <tr>
                        <td style="padding: 4px;">Notification sent by </td>
                        <td style="padding: 4px;">Shailesh Ubhe</td>
                    </tr>

                </tbody>
                <tfoot>
                    <tr>
                        <td colspan="2" style="padding: 4px;">This is an auto-generated email and reply to this mail id is not monitored. In case of any query please contact [shaileshubhe77@gmail.com]</td>
                        
                    </tr>
                </tfoot>
            </table>
            """,
       subject: """JenkinsNotification: ${status}:""", 
       to: 'shaileshubhe77@gmail.com'
           )
}

pipeline{
    agent any
    stages {
        //notify'Started')
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
        stage ('Artifacts'){
            steps {
                //notify ('Waiting for Deployment')
                //input 'Deploy to Staging?'
                archiveArtifacts 'target/*.war'
            }
        }

    }
 post {
    always {
    input 'Deploy to Staging?' 
    notify('completed') 
    //emailext body: 'build started', subject: 'build started', to: 'shaileshubhe77@gmail.com'
    }
  }
}
