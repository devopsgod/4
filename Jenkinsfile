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

    app = docker.build("config-service")
  }

  stage('Deploy image') {
    bat(script: 'C:\\Windows\\System32\\cmd.exe /c docker rm -f config-service-container')
    bat(script: 'C:\\Windows\\System32\\cmd.exe /c docker run -d -p 8000:8000 --name config-service config-service')
  }
}
