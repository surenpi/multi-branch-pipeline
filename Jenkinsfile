pipeline {
  agent any
  
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
          pullRequest.switchPullRequest(2).removeLabel('ready-for-merge')
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
  }
  
  post{
    always{
      print currentBuild.duration
    }
  }
}
