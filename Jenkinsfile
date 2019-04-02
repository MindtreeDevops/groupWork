@Library('my_shared_library')_
properties([parameters([string(defaultValue: 'add this job name', description: '', name: 'job', trim: false), gitParameter(branch: '', branchFilter: '.*', defaultValue: 'origin/master', description: '', name: 'Branch', quickFilterEnabled: false, selectedValue: 'NONE', sortMode: 'NONE', tagFilter: '*', type: 'PT_BRANCH')]), pipelineTriggers([upstream('example')])])
node {
    
    
    stage('install packer'){
       tool name: 'PACKER', type: 'com.cloudbees.jenkins.plugins.customtools.CustomTool' 
       
    }
    stage('Checkout external proj') {
        git branch: 'master',
            credentialsId: 'github',
            url: 'https://github.com/Devops-Accelerators/JenkinsSharedPipeline.git'
        

        sh "ls -lat"
    }
    
    stage('image create'){
         echo 'creating an image'
        packerexec "/var/lib/jenkins/workspace/${job}/resources/pack.json"
    }
    stage('instance creation'){
        echo 'creating an instance'   
        terraformexec "/var/lib/jenkins/workspace/${job}/terraform/"
    }
    stage('git remove'){
        sh "rm -rf /var/lib/jenkins/workspace/${job}/*"
    }
}
