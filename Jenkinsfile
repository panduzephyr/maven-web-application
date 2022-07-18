node
{
def mavenHome = tool name : "maven3.8.5"
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '5', artifactNumToKeepStr: '5', daysToKeepStr: '5', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
echo "The Job Name is: ${env.JOB_NAME}"
echo "The Job Name is: ${env.NODE_NAME}"
echo "The Job Name is: ${env.WORKSPACE}"
echo "The Job Name is: ${env.NODE_LABELS}"
echo "The Job Name is: ${env.NODE_NUMBER}"
echo "The Job Name is: ${env.BUILD_URL}"
stage('CheckoutCode')
{
git branch: 'qa', credentialsId: '67b36730-1097-4a12-8bbd-f63ce27c537b', url: 'https://github.com/panduzephyr/maven-web-application.git'
}
stage('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}
 /* 
stage('ExecuteSonarQubeRepot')
{
sh "${mavenHome}/bin/mvn clean sonar:sonar"
}
stage('UploadArtifactsIntoNexus')
{
sh "${mavenHome}/bin/mvn deploy"
}
stage('DeployAppIntoTomcatServer')
{
sshagent(['d0fe678d-d9a1-4eaa-b86c-c8fd4a888248']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.154.54.250:/opt/apache-tomcat-9.0.64/webapps"

}

} */
}
