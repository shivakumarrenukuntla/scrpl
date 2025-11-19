node('built-in') 
{
    stage('cntdownload') 
    {
    git branch: 'main', url: 'https://github.com/shivakumarrenukuntla/spl.git'
    }
        stage('contbuild')
    {
        sh 'mvn package'
    }
        stage('contdeployment')
        {
            sh '''
ssh root@172.31.72.35 "sudo mkdir -p /var/lib/tomcat10/webapps/"
scp /home/ubuntu/.jenkins/workspace/spl/webapp/target/webapp.war root@172.31.72.35:/var/lib/tomcat10/webapps/testpg.war
'''
         }
         stage('conttesting')
         {
            git 'https://github.com/shivakumarrenukuntla/FunctionalTesting.git'
            sh 'java -jar /home/ubuntu/.jenkins/workspace/spl_scm/testing.jar'
         }
         stage('contdelivery')
         {
             
            sh 'scp /home/ubuntu/.jenkins/workspace/spl/webapp/target/webapp.war root@172.31.72.35:/var/lib/tomcat10/webapps/userpg.war'
         }
    }
