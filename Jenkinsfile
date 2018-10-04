pipeline {//Declarative Syntax 

    //agent any
      agent { label 'Carlos' }
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
								
					//echo " ids= ${IDS} jaae"		
					//test -DUid=Nexus5,Nexus9
					
					//if("${Fuente}" == "Fisico"){
						//if ("${Plataforma}" == "Android" || "${Plataforma}" == "Iphone" ) {							
							git url: 'ssh://git@gitlab.awadserver.com:2222/esteban.berduo/combos_combinados.git'				
							bat "git checkout CIFactory2" 
							bat "git pull"
							bat "mvn clean test -DDevicename=${IDS}"									     					
							//bat "mvn clean test -DUid=${ID} "											   						
						//} else {
						//	echo 'web'
						//	git url: 'ssh://git@gitlab.awadserver.com:2222/esteban.berduo/combos_combinados.git'				
						//	bat "git checkout CIFactory" 
						//	bat "git pull"
						//	bat "mvn clean test -DBrowser=${Navegador} -DPlatform=${Plataforma}"
						//}
					//}										
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
