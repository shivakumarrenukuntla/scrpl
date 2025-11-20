node('built-in') {
    stage('Checkout Code') {
        git branch: 'main', url: 'https://github.com/shivakumarrenukuntla/spl.git'
    }

    stage('Build') {
        sh 'mvn package'
    }

    stage('Deploy to Tomcat') {
        // Use SSH private key in Jenkins credentials
        withCredentials([sshUserPrivateKey(credentialsId: 'ssh-key-ec2', keyFileVariable: 'SSH_KEY')]) {
            sh """
                ssh -i $SSH_KEY -o StrictHostKeyChecking=no root@172.31.72.35 "sudo mkdir -p /var/lib/tomcat9/webapps/"
                scp -i $SSH_KEY -o StrictHostKeyChecking=no /home/ubuntu/.jenkins/workspace/spl/webapp/target/webapp.war root@172.31.72.35:/var/lib/tomcat9/webapps/testpg.war
            """
        }
    }

    stage('Functional Testing') {
        git 'https://github.com/shivakumarrenukuntla/FunctionalTesting.git'
        sh 'java -jar /home/ubuntu/.jenkins/workspace/spl_scm/testing.jar'
    }

    stage('Delivery') {
        withCredentials([sshUserPrivateKey(credentialsId: 'ssh-key-ec2', keyFileVariable: 'SSH_KEY')]) {
            sh """
                scp -i $SSH_KEY -o StrictHostKeyChecking=no /home/ubuntu/.jenkins/workspace/spl/webapp/target/webapp.war root@172.31.72.35:/var/lib/tomcat9/webapps/userpg.war
            """
        }
    }
}
