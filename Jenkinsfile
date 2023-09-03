node
{
def mavenHome = tool name : "maven3.8.5"
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '1', daysToKeepStr: '', numToKeepStr: '1')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
echo "The Job Name is: ${env.JOB_NAME}"
echo "The Node Name is: ${env.NODE_NAME}"
echo "The Work Space Path is: ${env.WORKSPACE}"
echo "The Node Labels Name is: ${env.NODE_LABELS}"
echo "The Node Number is: ${env.NODE_NUMBER}"
echo "The Build URL is: ${env.BUILD_URL}"
stage('CheckoutCode')
{
git branch: 'development', credentialsId: '740cb0ee-78de-4fbb-8d47-f067503addcb', url: 'https://github.com/panduzephyr/maven-web-application.git'
}
stage('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}
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
sshagent(['064d97c7-e040-4b50-9d64-ba4b45ffc764']) {
    
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.1.2.120:/opt/apache-tomcat-9.0.79/webapps/"

}

}
}

