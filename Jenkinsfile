node {
  def app

  stage('Clone repository') {
    /* Let's make sure we have the repository cloned to our workspace */

    checkout([$class: 'GitSCM', branches: [[name: '*/master']], 
    doGenerateSubmoduleConfigurations: false, 
    extensions: [], submoduleCfg: [], 
    userRemoteConfigs: [[url: 'https://github.com/devopsgod/4']]])
  }

  stage('Build image') {
  /* This agent directive tells Jenkins to allocate an executor and workspace for the pipeline on any available agent */

  app = docker.build("myapp")
}

stage('Deploy image') {
  /* This image parameter (of the agent directive) tells Jenkins to use the Docker image, which was previously built, as the execution environment for this stage */

  bat(script: 'C:\\Windows\\System32\\cmd.exe /c docker run -d -p 8000:8000 myapp')
}

}