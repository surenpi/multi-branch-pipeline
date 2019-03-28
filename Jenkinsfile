pipeline {
  agent any
  
  stages{
    stage("one") {
      steps{
        echo "one"
        echo "BRANCH_NAME" + env.BRANCH_NAME
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
        branch '*test*'
      }
      steps{
        echo "three"
      }
    }
  }
}
