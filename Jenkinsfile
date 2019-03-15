pipeline {
  agent any
  
  stages{
    stage("one") {
      steps{
        echo "one"
      }
    }
    
    stage("two"){
      when {
        anyOf {
          changeset '**/*.js'
          changeset '**/*.html'
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
