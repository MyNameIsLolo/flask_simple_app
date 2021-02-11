node {
   def commit_id
   stage('Preparation') {
     checkout scm
     sh "git rev-parse --short HEAD > .git/commit-id"
     commit_id = readFile('.git/commit-id').trim()
   }
   stage('test') {
     def myTestContainer = docker.image('python')
     myTestContainer.pull()
     myTestContainer.inside('-u root') {
       sh 'pip install -r requirements.txt'
       sh 'pytest -v'
     }
   }   
   stage('sonar-scanner') {
      def sonarqubeScannerHome = tool name: 'sonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
      withSonarQubeEnv('sonarqube_server') {
        sh "${sonarqubeScannerHome}/bin/sonar-scanner"
      }
    }                                  
   stage('docker build/push') {            
     docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
       def app = docker.build("lniviere/flask_simple_app:${commit_id}", '.').push()
     }                                     
   }                                       
}  
