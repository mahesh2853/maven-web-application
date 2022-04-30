node{

echo "Job Name is: ${env.JOB_Name}"
echo "Node Nmae is: ${env.NODE_NAME}"


def mavenHome = tool name: 'maven3.8.4'

//Get the code from Github Repo
stage('CheckoutCode'){
git branch: 'development', credentialsId: 'g', url: 'https://github.com/mahesh2853/maven-web-application.git'

}
//Do the build by using Maven Build tool
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
*/
//Execute the SonarQube Report
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"
}

//Upload Artifacts into Artifactory Repo
stage('UploadArtifactsintoNexus'){
sh "${mavenHome}/bin/mvn deploy"
}

//Deploy Application into Tomcat Server
stage('DeployApplicationIntoTomcatServer'){
sshagent(['304675f1-190d-432d-89de-6a7e595d2bbf']) {
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@15.206.195.58:/opt/apache-tomcat-9.0.62/webapps/"

}
}
/* 
}
