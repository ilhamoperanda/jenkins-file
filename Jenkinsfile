
pipeline {
    agent any

    parameters {
        string(name: 'RFC', defaultValue: 'RFC_12345', description: '')
        
        choice(name: 'BRANCH', choices: ['feature', 'release'], description: '')
        
        string(name: 'REPO', defaultValue: '1p_ciforigination', description: '')
        
    }

    stages {
        stage('Create Dir Project') {
            steps {
                bat """
                    if exist D:\\CN036842\\Project\\${params.RFC} (
                        mkdir D:\\CN036842\\Project\\${params.RFC}\\source\\git\\${params.BRANCH}\\${params.REPO}
                    ) else (
                        mkdir D:\\CN036842\\Project\\${params.RFC}
                        mkdir D:\\CN036842\\Project\\${params.RFC}\\source
                        mkdir D:\\CN036842\\Project\\${params.RFC}\\source\\git
                        mkdir D:\\CN036842\\Project\\${params.RFC}\\source\\git\\${params.BRANCH}
                        mkdir D:\\CN036842\\Project\\${params.RFC}\\source\\git\\${params.BRANCH}\\${params.REPO}
                        mkdir D:\\CN036842\\Project\\${params.RFC}\\doc   
                        mkdir D:\\CN036842\\Project\\${params.RFC}\\workspace\\ace\\static   
                        mkdir D:\\CN036842\\Project\\${params.RFC}\\workspace\\ace\\shared   
                        mkdir D:\\CN036842\\Project\\${params.RFC}\\workspace\\iib10\\static   
                        mkdir D:\\CN036842\\Project\\${params.RFC}\\workspace\\iib10\\shared   
                    )
                """  
                echo "SUCCESS create dir D:\\CN036842\\Project\\${params.RFC}\\source\\git\\${params.BRANCH}\\${params.REPO}"
                echo "SUCCESS create dir D:\\CN036842\\Project\\${params.RFC}\\doc   "
            }
        }
        stage('Git Clone') {
            steps {

                checkout([$class: 'MercurialSCM', credentialsId: 'svn-cred', source: 'https://idcbuesbdbs001.mylab.local:8443/svn/ESB_ID_Project/ESB_RFC2913011_WMOnboardingOS_DOC'])
                git branch: "${params.BRANCH}/${params.RFC}", 
					credentialsId: '2ea347b8-e704-4ccf-9b0f-7c087c762377', 
					url: "https://bitbucket.cimbniaga.co.id/scm/eib/${params.REPO}.git"
				
                echo "git clone from branch : ${params.BRANCH}/${params.RFC}"
                echo "git clone url : https://bitbucket.cimbniaga.co.id/scm/eib/${params.REPO}.git"

                echo "SUCCESS"
                
                echo "copy from workspace jenkins to dir project"
                bat "xcopy /e /v C:\\Users\\IO36842X\\.jenkins\\workspace\\git_clone_iib D:\\CN036842\\Project\\${params.RFC}\\source\\git\\${params.BRANCH}\\${params.REPO}"

           
                
                echo "SUCCESS"

                
		
            }
        }
       
       
    }
}
