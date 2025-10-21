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
/*sonarQube Report generation 
stage('SonarQube Report') {
sh "$mavenHome/bin/mvn sonar:sonar"
    }
*/
//uploading artifact into nexus repo
stage('uploading artifact'){
sh "$mavenHome/bin/mvn deploy"    
}
//deploy app into tomcat 
stage('Deploy app into Tomcat'){
 sshagent(['c8660d04-098a-4e18-8771-691d9511294f']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@54.221.41.102:/opt/tomcat/webapps"
}   
}
}










