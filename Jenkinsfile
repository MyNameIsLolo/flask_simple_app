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
     myTestContainer.inside {
       sh 'python --version'
     }
   } 
}