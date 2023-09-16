// use this to write comment in pipeline
pipeline{
    
    tools{ 
        // This section is not mandatory
        // in this block we declare the names of tools used during the pipeline
        // the name comes from the global tool configuration set up
        maven 'mymaven'
    }
    
    // which VM should we execute this pipeline
    // agent = VM
    // any = any available VM that jenkins is connected to.
    // Right now jenkins is associated to lab server
    // This is a mandatory section
    agent any
    
    stages{    // here we create multiple stage
    // each stage =jenkins job
        stage('Clone Repo')
        {
            // In this stage we are going to clone entire repo in jenkins workspace
            steps{
                git 'https://github.com/Sonal0409/DevOpsCodeDemo.git'
            }
        }
        
        stage('Build the code')
        {
            steps{
                sh 'mvn clean install package'
                // clean: clean the target folder of maven. clean previous build files
                // install: it will install any softwares needed for code to build
                //package: compile, test and package the code.
                // ouput is going to be a artifact
            }
        }
        
        stage('Build Image'){
            steps{
                sh 'cp /var/lib/jenkins/workspace/CICDPipeline/target/addressbook.war .'
                sh 'docker build -t myappimage .'
            }
        }
        
        stage('Deploy the App'){
            steps{
                sh 'docker run -d -P myappimage'
            }
        }
    }
    
    
    
    
}
