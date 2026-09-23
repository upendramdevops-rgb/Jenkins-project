In Jenkins, there are fundamentally two main types of pipelines: Declarative and Scripted.

The pipeline you just wrote is a Declarative Pipeline. Here is a breakdown of both, their differences, and a few related concepts you should know.

1. Declarative Pipeline (What you are using)
This is the modern, recommended way to write pipelines. It was introduced to make pipelines easier to read and write. It has a strict, predefined structure.

Syntax: Must start with pipeline { }.

Structure: Uses specific blocks like agent, stages, steps, environment, and post.

Error Handling: Has a built-in post section for handling success/failure.

Visualization: Works perfectly with the Jenkins Blue Ocean UI.

Example:

groovy
pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
    }
    post {
        always {
            echo "Pipeline finished."

2. Scripted Pipeline
   
This is the original way to write pipelines. It is essentially a full Groovy script. It gives you maximum flexibility but is harder to learn and read.

Syntax: Must start with node { }.

Structure: Uses pure Groovy code. You can use if/else, for loops, try/catch blocks, and define custom functions.

Error Handling: You must manually use try/catch/finally to handle errors.

Visualization: Does not visualize as nicely in Blue Ocean.

Example:

groovy
node {
    try {
        stage('Build') {
            sh 'mvn clean package'
        }
    } catch (Exception e) {
        echo "Build failed: ${e}"
    } finally {
        echo "Pipeline finished."
    }
}
        }
    }
}
