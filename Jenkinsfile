       try {
    library(
        identifier: 'jsl-jenkins-shared-library@master',
        retriever: modernSCM(
        [
              $class: 'GitSCMSource',
              remote: "https://github.com/CenturyLink/jsl-jenkins-shared-library.git",
              credentialsId: 'SCMAUTO_GITHUB',
              extensions: [[$class: 'WipeWorkspace']]
        ])
    ) _
} catch (Exception Ex) {
    library(
        identifier: 'jsl-jenkins-shared-library-local@master',
       retriever: modernSCM(
        [
              $class: 'GitSCMSource',
              remote: "/app/jenkins/git/jsl-jenkins-shared-library.git",
              extensions: [[$class: 'WipeWorkspace']]
        ])
    ) _
}
pipeline {
   agent {
	label 'Docker-enabled'
	}
	environment {
	  git_url = "git@dc2gitlab1.mgmt.savvis.net:huge-automation-and-scripts/goc-handover.git"
	  service_name = "windowsunix"
	  remote_pass = credentials('gocdash_jenkins')
	  devuser = "gocdash_jenkins"
	  devhost = "dc2iws1.it.savvis.net"

    dev_server_path = "/data02/websites/devgocdashboard/htdocs"
    
    release_server_path = "/data02/websites/releasegocdashboard/htdocs"

    master_server_path = "/data02/websites/prodgocdashboard/htdocs"
  }
  stages {
      
	  stage("code checkout") {
      steps { checkout scm
              checkout([$class: 'GitSCM', 
              branches: [[name: env.BRANCH_NAME]], 
              doGenerateSubmoduleConfigurations: false, 
              extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: "${service_name}"]], 
              gitTool: 'Default',
              submoduleCfg: [], 
              userRemoteConfigs: [[credentialsId: '26a14b93-d2f5-48b6-85ad-815ac20027e4', url: "${git_url}"]]])
    }}
}

