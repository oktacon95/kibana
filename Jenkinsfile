timestamps {

 node () {

  stage ('checkout repository') {
   checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'GitHub_User', url: 'https://github.com/oktacon95/kibana']]]) 
  }
  stage ('build docker image') {
   sh "docker build -t mykibana ." 
  }
  stage ('stop old docker image') {
   sh "docker stop kibana" 
  }
  stage ('create new docker container') {
   sh 'docker run -d --rm --name kibana -v /etc/kibana/config:/usr/share/kibana/config --network elknet -p 5601:5601 mykibana'
  }
 }
}
