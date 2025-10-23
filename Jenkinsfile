node{
def mavenHome = tool name: "maven3.9.11"
//Checkout Stage
stage('CheckoutCode'){
git branch: 'development', url: 'https://github.com/Sakhtar-8254/maven-web-application.git'
}
//Build Stage
stage('Build'){
sh "$mavenHome/bin/mvn clean package"
}
//sonarQube Report generation 
stage('SonarQube Report') {
sh "$mavenHome/bin/mvn sonar:sonar"
    }
//uploading artifact into nexus repo
stage('uploading artifact'){
sh "$mavenHome/bin/mvn deploy"    
}
//deploy app into tomcat 
stage('Deploy app into Tomcat'){
sshagent(['217ca659-5c98-4cae-992c-194d0512b727']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@34.233.136.133:/opt/tomcat/webapps"
}   
}
}










