#!groovy
@Library('mechanoidstore-shared-library') _

// we neet to set the parameters to pass what type of app and component is this to pipeline decision in shared library directory.

def configMap = [
    application: "nodejsVM",
    component: "catalogue"
]

if( ! env.BRANCH_NAME.equalsIgnoreCase('master')){
    pipelineDecision.decidePipeline(configMap)
}
else{
    echo "This is Production, deal with CR process"
}