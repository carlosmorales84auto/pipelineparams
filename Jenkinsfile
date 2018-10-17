pipeline {//Declarative Syntax 

    //agent any
    //agent { label 'Carlos' }
	agent { node { label "${Nodo}" } }
	//agent { node { label 'CarlosMac' } }
    //tools {
       // maven 'LocalMaven' 
    //}
    options {
        timeout(time: 10, unit: 'MINUTES') //tiempo maximo de ejecucion del pipeline
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
				    mvn -version
				    mvn clean test -DDevicename=${IDS}				    
				'''
				echo 'termina corriendo en la mac'
			}else{			
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
