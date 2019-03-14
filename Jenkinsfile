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
        changeset '**/*.js'
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
