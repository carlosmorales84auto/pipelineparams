pipeline {//Declarative Syntax 

    //agent any
    //agent { label 'Carlos' }
	agent { node { label "${Nodo}" } }
	//agent { node { label 'CarlosMac' } }
    tools {
        maven 'LocalMaven' 
    }
    options {
        timeout(time: 3, unit: 'MINUTES') //tiempo maximo de ejecucion del pipeline
    }
	environment { 
        VarGlobal = 'soy una variable global'
    }	
    stages {	    	  
	stage('Smartphone') {
            steps {
		script {
			echo 'Before checkout report'
			git url: 'ssh://git@gitlab.awadserver.com:2222/esteban.berduo/combos_combinados.git'				
			echo "After checkout report"
			
			if("${Nodo}" == "CarlosMac"){
				echo 'corriendo en la mac'			
				sh '''
				    git checkout CIFactory2
				    git pull
				    mvn -version
				    mvn clean test -DDevicename=${IDS}				    
				'''
				echo 'termina corriendo en la mac'
			}else{			
				bat "git checkout CIFactory2" 
				bat "git pull"
				bat "mvn clean test -DDevicename=${IDS}"
			}
		}
            }
        }

    }
	post { 
		success{
			echo 'Pruebas exitosas!'
		}
		failure{
			echo '**************Algo fallo!!!!'
		}
		always { 
            echo "build: ${currentBuild.fullDisplayName}"
        }
    }
}
