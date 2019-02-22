pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
                git 'https://github.com/selenium-saikrishna/maven.git'
            }
        }
        stage('ContBuild')
        {
            steps
            {
                sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
                sh 'scp /home/ubuntu/.jenkins/workspace/Declarative_Pipeline/webapp/target/webapp.war ubuntu@172.31.28.230:/var/lib/tomcat8/webapps/qaenv.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/selenium-saikrishna/FunctionalTesting.git'
                sh 'java -jar  /home/ubuntu/.jenkins/workspace/Declarative_Pipeline/testing.jar'
            }
        }
    }
    post
    {
        success
        {
            input message: 'Waiting for approval from DM', submitter: 'brajesh'
    sh 'scp /home/ubuntu/.jenkins/workspace/Declarative_Pipeline/webapp/target/webapp.war ubuntu@172.31.20.225:/var/lib/tomcat8/webapps/prodenv.war'
        }
        failure
        {
            mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'Build failed', to: 'brajeshmodi26@gmail.com'
            
        }
        
     }
}
