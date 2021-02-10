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
       sh 'python --version'
       sh 'pwd'
       sh 'pip install -r requirements.txt'
       sh 'pytest --version'
       sh 'pytest -v'
     }
   }                                     
   stage('docker build/push') {            
     docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
       def app = docker.build("lniviere/docker-nodejs-demo:${commit_id}", '.').push()
     }                                     
   }                                       
}  