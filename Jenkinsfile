pipeline {
    agent any
    environment {
        ENV_NAME = 'Arithmatic Operation'
		SERVICE_NAME= 'Firstprogram'
        MSBuild = '\"C:/Program Files/Microsoft Visual Studio/2022/Community/MSBuild/Current/Bin/MSBuild.exe\"'
		ARTIFACT_ZIP='ArithmaticOperation.zip'
		ARTIFACT_ZIP_DIR='C:/projects/outdir'
		OUTDIR='C:/projects/outdir/ArithmaticOperation/'
    }
    parameters {
		string defaultValue: 'Calculator', description: 'Arithmatic Operation', name: 'APPLICATION_NAME', trim: true
	}
	stages {
		stage('CleanWorkspace') {
            steps { cleanWs() }
        }
        stage('CreateDIR') {
            steps {
				script {
					println "INFO: Creating $ARTIFACT_ZIP_DIR"
					powershell "Remove-Item $ARTIFACT_ZIP_DIR/* -Recurse -Force"
					powershell "New-Item -Path $OUTDIR -ItemType Directory"
				} 
			}
        }
        stage('MsBuild:Clean') {
            steps {
                script {
						bat "$MSBuild C:/projects/code/Firstprogram/Firstprogram.sln /t:build /p:Configuration=Release /m /p:OutputPath=$OUTDIR -noconlog"
					}
                }
        }
        stage ('zipFolder'){
			steps {
                script {
						 println "Artifact Folder: $OUTDIR"
						 println "Artifact Zip Folder: $ARTIFACT_ZIP_DIR"
						 println "Artifact Zip : $ARTIFACT_ZIP"
						 println "Service Name: $SERVICE_NAME"
						 println "Compressing: $OUTDIR$SERVICE_NAME"
                         powershell "Compress-Archive $OUTDIR $ARTIFACT_ZIP_DIR$ARTIFACT_ZIP"
					}
                }
            }
	}
}
