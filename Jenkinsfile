node('master'){
    def mavenHome = tool name:"mvn363"
    stage('get the Code from Git'){
        git branch: 'development', url: 'https://github.com/mmuralim/maven-web-application.git'
    }
    
    stage('Compile and Build the code'){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('Execute Sonarqube Report'){
        sh "${mavenHome}/bin/mvn sonar:sonar" 
    }
    stage('Upload Artifacts to Nexus'){
        sh "${mavenHome}/bin/mvn deploy" 
    }
    stage('Deploy to Tomcat app server'){
    //    sshagent(['tomcatServerCredentials']) {
    //    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war    vagrant@192.168.29.46:/opt/tomcat/webapps/"
    //    }
    //    sshagent(['TomcatCreds']) {
    //        sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war    vagrant@192.168.29.46:/opt/tomcat/webapps/"
    //    }
    //    sshagent(['tomcatServerCredentials']) {
    //    sh "scp -vvv -o StrictHostKeyChecking=no target/maven-web-application.war    vagrant@192.168.29.46:/opt/tomcat/webapps/"
    //    }
        sshagent(['tomcatServerCredentials']) {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war    vagrant@192.168.29.46:/opt/tomcat/webapps/"
        }
    }
    stage('Send Email notification'){
        mail bcc: '', body: 'Build completed ....', cc: '', from: '', replyTo: '', subject: 'Email notification of the pipeline job', to: 'pavanim1987@gmail.com'
    }
}
