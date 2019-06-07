pipeline {
  agent {
    label 'master'
  }
  
  stages{
    stage("one") {
      when {
        changeRequest()
      }
      steps{
        echo "one"
        echo "BRANCH_NAME" + env.BRANCH_NAME
        
        script {
          pullRequest.addLabel('testing')
          
          pullRequest.switchPullRequest(2).addLabel('testing')
        }
      }
    }
    
    stage("two"){
      when {
        anyOf {
          changeset '**/**/*.js'
          changeset '**/**/*.html'
        }
      }
      steps{
        echo "take care of js files"
      }
    }
    
    stage("three") {
      when {
        branch 'master'
      }
      steps{
        echo "master"

        script {
          pullRequest.removeLabel('ready-for-merge')
        }
      }
    }
    
    stage("four") {
      when {
        branch '*test*'
      }
      steps{
        echo "three"
      }
    }

    stage("release") {
      when {
        tag pattern: "release-.*", comparator: "REGEXP"
      }
      steps{
        echo "released successfully"
      }
    }
    
    stage("files"){
      steps{
        script{
          for (commitFile in pullRequest.files) {
              echo "SHA: ${commitFile.sha} File Name: ${commitFile.filename} Status: ${commitFile.status}"
          }
        }
      }
    }
  }
  
  post{
    always{
      print currentBuild.duration
    }
  }
}
